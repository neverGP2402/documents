# 1.Create a new user 
Step 1: create user name
```vim
    useradd -c "user_name" user_name
```
Step 2: Set password
```vim
    useradd -c "pass_word" pass_word
```
# 2. Compress and decompress 
## Compress: 
```vim
    tar -zcvf folder_name.tar.gz * 
```
## Decompress: 
```vim
    tar -xzvf folder_name.tar.gz
```

# 3. Install pgsql 13 (Install the repository RPM) https://www.postgresql.org/download/linux/redhat/

### Step 1: Cài đặt kho lưu trữ PostgreSQL chính thức/ Setup the built-in PostgreSQL module
```vim
    sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

### Step 2: Disable the built-in PostgreSQL module/Vô hiệu hóa kho PostgreSQL mặc định:
```vim
    sudo dnf -qy module disable postgresql
```

### Step 3: Install PostgreSQL:
```vim
    sudo dnf install -y postgresql13-server
```
### Step 4: Optionally initialize the database and enable automatic start/Tùy chọn khởi tạo cơ sở dữ liệu và cho phép khởi động tự động:
```vim
    sudo /usr/pgsql-13/bin/postgresql-13-setup initdb
    sudo systemctl enable postgresql-13
    sudo systemctl start postgresql-13
```
# 4. CREATE USER AND DATABASE PGSQL (Using user root)

```vim
    su - postgres
    psql
    CREATE user user_db;
    ALTER USER user_db PASSWORD 'password';
    CREATE DATABASE db_name OWNER user_db;
```

# 5. Config NGINX (Using user root)
### Step 1: initialize server configuration in file `nginx.conf` path: `/etc/nginx/nginx.conf`
```
server {
    listen       80;
    listen       [::]:80;

    server_name  skm-dev.chips.com.vn;

    if ($host = 'skm-dev.chips.com.vn') {
        return 301 https://skm-dev.chips.com.vn$request_uri;
    }
}
server {
    listen       443 ssl;
    listen       [::]:443 ssl;
    server_name  skm-dev.chips.com.vn;
    root         /home/skmerp_web/src/client;

    ssl_certificate "/etc/pki/tls/certs/ssl_bundle.chips.com.vn.crt";
    ssl_certificate_key "/etc/pki/tls/private/ssl.chips.com.vn.key";
    ssl_session_cache shared:SSL:1m;
    ssl_session_timeout  10m;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    client_max_body_size 200M;

    location / {
        # using http - restful method
        root /home/skmerp_web/src/client;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_http_version 1.1;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;

        proxy_buffers 16 32k;
        proxy_buffer_size 64k;
        proxy_busy_buffers_size 128k;
        proxy_headers_hash_max_size 512;
        proxy_headers_hash_bucket_size 128;

        proxy_cache_bypass $http_pragma $http_authorization;
        proxy_connect_timeout 59s;
        proxy_hide_header X-Powered-By;
        proxy_ignore_headers Cache-Control Expires;

        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504 http_404;
        proxy_no_cache $http_pragma $http_authorization;
        proxy_pass_header Set-Cookie;
        proxy_read_timeout 600;
        proxy_redirect off;

        proxy_send_timeout 600;
        proxy_temp_file_write_size 64k;
        proxy_set_header Accept-Encoding '';
        proxy_set_header Cookie $http_cookie;
        proxy_set_header Proxy '';
        proxy_set_header Referer $http_referer;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Server $host;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Original-Request $request_uri;
        proxy_pass http://skm-dev.chips.com.vn:3162;
    }

    location /skm_sv {
        rewrite ^/skm_sv/(.*) /socket.io/$1 break;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_http_version 1.1;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        # proxy_pass: sẽ thực hiện gửi request tới một proxy server cụ thể. 
        proxy_pass http://skm-dev.chips.com.vn:3163;
    }
}
```

### Step 2: Check nginx configuration
```vim
    nginx -t
```

### Step 3: Restart nginx 

```vim
    sudo systemctl reload nginx
```