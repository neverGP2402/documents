1. Kiểm tra xem RabbitMQ có được cài đặt hay chưa:
Trước tiên, hãy kiểm tra liệu RabbitMQ đã được cài đặt trên hệ thống hay chưa.

```bash
rabbitmqctl status
```
Nếu RabbitMQ không được cài đặt, bạn có thể tiến hành cài đặt.

2. Cài đặt RabbitMQ trên AlmaLinux:
Bạn có thể cài đặt RabbitMQ bằng các bước sau:

a. Thêm kho lưu trữ EPEL:
Trên AlmaLinux, bạn cần thêm kho EPEL trước khi cài đặt RabbitMQ:

```bash
sudo dnf install epel-release
```
b. Thêm kho lưu trữ RabbitMQ:
Thêm kho lưu trữ của RabbitMQ:

```bash
sudo tee /etc/yum.repos.d/rabbitmq_erlang.repo <<EOF
[rabbitmq_erlang]
name=rabbitmq_erlang
baseurl=https://dl.cloudsmith.io/public/rabbitmq/rabbitmq-erlang/rpm/el/8/\$basearch
gpgcheck=1
gpgkey=https://dl.cloudsmith.io/public/rabbitmq/rabbitmq-erlang/gpg.key
enabled=1

[rabbitmq_rabbitmq-server]
name=rabbitmq_rabbitmq-server
baseurl=https://dl.cloudsmith.io/public/rabbitmq/rabbitmq-server/rpm/el/8/\$basearch
gpgcheck=1
gpgkey=https://dl.cloudsmith.io/public/rabbitmq/rabbitmq-server/gpg.key
enabled=1
EOF
```
c. Cài đặt Erlang và RabbitMQ:
Cài đặt Erlang, vì RabbitMQ yêu cầu nó để hoạt động.

```bash
sudo dnf install erlang
```
Sau đó cài đặt RabbitMQ:

```bash
sudo dnf install rabbitmq-server
```
3. Khởi động và kích hoạt RabbitMQ:
Sau khi cài đặt, khởi động và kích hoạt dịch vụ RabbitMQ:

```bash
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server
```
4. Kiểm tra lại trạng thái RabbitMQ:
Sau khi khởi động, bạn có thể kiểm tra lại trạng thái RabbitMQ:

```bash
sudo systemctl status rabbitmq-server
```
Thực hiện các bước sau để cài đặt RabbitMQ từ gói RPM:
1. Tải Erlang từ kho RabbitMQ:
Vì Erlang đã được cài đặt thành công, bạn có thể bỏ qua bước này.

2. Tải xuống RabbitMQ Server RPM:
Tải gói RabbitMQ RPM trực tiếp từ trang web RabbitMQ:

```bash
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.12.5/rabbitmq-server-3.12.5-1.el8.noarch.rpm
```
3. Cài đặt gói RabbitMQ:
Cài đặt RabbitMQ từ file RPM đã tải về:

```bash
sudo dnf localinstall rabbitmq-server-3.12.5-1.el8.noarch.rpm
```
4. Khởi động và kích hoạt RabbitMQ:
Sau khi cài đặt, khởi động dịch vụ RabbitMQ và kích hoạt nó để chạy tự động khi khởi động:

```bash
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server
```
5. Kiểm tra trạng thái của RabbitMQ:
Kiểm tra trạng thái của RabbitMQ để đảm bảo nó đang hoạt động:

```bash
sudo systemctl status rabbitmq-server
```
Lệnh wget chưa được cài đặt trên hệ thống của bạn. Bạn có thể cài đặt wget trước khi tải xuống RabbitMQ. Thực hiện lệnh sau:

```bash
sudo dnf install wget
```
Sau khi cài đặt thành công, bạn có thể tiếp tục tải gói RabbitMQ như đã hướng dẫn trước đó:

```bash
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.12.5/rabbitmq-server-3.12.5-1.el8.noarch.rpm
```
Nếu không muốn cài đặt wget, bạn có thể sử dụng curl để tải tệp về như sau:

```bash
curl -LO https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.12.5/rabbitmq-server-3.12.5-1.el8.noarch.rpm
```