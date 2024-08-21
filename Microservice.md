# Overview

## 1. Microservice là gì?. Và khi nào thì nên sử dụng?.
- `Microservice` là một kiến trúc phần mềm trong đó một ứng dụng được chia nhỏ thành các dịch vụ độc lập, mỗi dịch vụ thực hiện một chức năng cụ thể. Mỗi dịch vụ có thể được phát triển, triển khai và mở rộng riêng biệt, thường giao tiếp với nhau qua các API.

- Khi nào nên sử dụng Microservice?
    - `Tính mở rộng:` Khi ứng dụng cần mở rộng, microservice cho phép mở rộng các phần riêng lẻ theo nhu cầu.
    - `Quy mô lớn:` Với ứng dụng phức tạp, việc chia nhỏ thành các dịch vụ giúp quản lý và phát triển dễ dàng hơn.
    - `Đội ngũ phát triển phân tán:` Microservice cho phép các nhóm khác nhau làm việc trên các dịch vụ khác nhau mà không làm ảnh hưởng đến nhau.
    - `Công nghệ đa dạng:` Nếu bạn muốn sử dụng các công nghệ khác nhau cho từng dịch vụ, microservice là lựa chọn tốt.
    - `Triển khai linh hoạt:` Các dịch vụ có thể được triển khai độc lập, giúp cập nhật và sửa lỗi dễ dàng hơn.
- Khi nào không nên sử dụng Microservice?
    - `Ứng dụng nhỏ:` Khi ứng dụng không quá phức tạp, microservice có thể làm tăng độ phức tạp quản lý.
    - `Nhu cầu ổn định:` Nếu yêu cầu không thay đổi nhiều, một kiến trúc đơn giản hơn có thể hợp lý hơn.
    - `Khi thiếu kỹ năng:` Nếu đội ngũ chưa quen với microservice, việc chuyển đổi có thể gây khó khăn.
## 2. Cách giao tiếp giữa các service.
- `1. HTTP/REST`
    - `Mô tả:` Giao tiếp qua các API RESTful sử dụng HTTP/HTTPS.
    - `Ưu điểm:` Đơn giản, dễ hiểu và hỗ trợ nhiều ngôn ngữ lập trình.
    - `Nhược điểm:` Chậm hơn trong một số trường hợp do overhead của HTTP.
- `2. gRPC`
    - `Mô tả:` Sử dụng giao thức RPC (Remote Procedure Call) với Google Protocol Buffers.
    - `Ưu điểm:` Hiệu suất cao, hỗ trợ nhiều ngôn ngữ, và tự động hóa trong việc tạo mã.
    - `Nhược điểm:` Khó hơn trong cài đặt và triển khai so với REST.
- `3. Message Queues`
    - `Mô tả:` Giao tiếp qua hàng đợi tin nhắn như RabbitMQ, Kafka.
    - `Ưu điểm:` Giảm độ liên kết, cho phép xử lý bất đồng bộ và tăng tính chịu tải.
    - `Nhược điểm:` Thêm độ phức tạp trong việc quản lý và theo dõi.
- `4. Events`
    - `Mô tả:` Sử dụng cơ chế pub/sub (publish/subscribe) để truyền tải thông tin giữa các dịch vụ.
    - `Ưu điểm:` Khả năng mở rộng và tính linh hoạt cao.
    - `Nhược điểm:` Khó theo dõi và debugging hơn so với các phương thức đồng bộ.
- `5. GraphQL`
    - `Mô tả:` Cung cấp một API cho phép người dùng yêu cầu chính xác dữ liệu cần thiết.
    - `Ưu điểm:` Giảm thiểu số lượng lần gọi API và tải dữ liệu thừa.
    - `Nhược điểm:` Cần có hiểu biết sâu hơn về cấu trúc dữ liệu.
## 3. Các giải pháp quản lý khi có nhiều service giao tiếp với nhau.
- `1. API Gateway`
    - `Mô tả`: Sử dụng API Gateway để làm giao diện duy nhất cho tất cả các service.
    - `Lợi ích:` Tập trung hóa việc quản lý API, cải thiện bảo mật và đơn giản hóa giao tiếp.
- `2. Service Discovery`
    - `Mô tả`: Triển khai công cụ như Eureka hoặc Consul để tự động phát hiện và cấu hình các service.
    - `Lợi ích:` Giúp các service tìm thấy nhau mà không cần cấu hình thủ công, giảm thiểu sai sót.
- `3. Synchronous vs Asynchronous Communication`
    - `Mô tả`: Lựa chọn giữa giao tiếp đồng bộ (HTTP/REST, gRPC) và bất đồng bộ (message queues, event streams).
    - `Lợi ích:` Giao tiếp bất đồng bộ giúp giảm độ liên kết và cải thiện khả năng mở rộng.
- `4. Message Brokers`
    - `Mô tả`: Sử dụng message brokers như RabbitMQ hoặc Kafka để quản lý và truyền tải tin nhắn giữa các service.
    - `Lợi ích:` Giúp xử lý dữ liệu bất đồng bộ và tăng tính chịu lỗi của hệ thống.
- `5. Load Balancing`
    - `Mô tả`: Cấu hình cân bằng tải để phân phối lưu lượng đến nhiều phiên bản của từng service.
    - `Lợi ích:` Cải thiện tính khả dụng và hiệu suất của hệ thống.
- `6. Distributed Tracing`
    - `Mô tả`: Sử dụng công cụ như Zipkin hoặc Jaeger để theo dõi và phân tích lưu lượng giao tiếp giữa các service.
    - `Lợi ích:` Giúp xác định điểm nghẽn và tối ưu hóa hiệu suất.
- `7. Circuit Breaker Pattern`
    - `Mô tả`: Áp dụng mẫu Circuit Breaker để quản lý lỗi và ngăn chặn lỗi lan rộng giữa các service.
    - `Lợi ích:` Tăng cường tính ổn định và khả năng phục hồi của hệ thống.
- `8. Centralized Configuration Management`
    - `Mô tả`: Sử dụng quản lý cấu hình trung tâm như Spring Cloud Config để đồng bộ hóa cấu hình giữa các service.
    - `Lợi ích:` Dễ dàng quản lý và cập nhật cấu hình cho toàn bộ ứng dụng.
- `9. Monitoring and Logging`
    - `Mô tả`: Thiết lập các công cụ giám sát và ghi log như ELK Stack hoặc Prometheus để theo dõi hiệu suất và sự cố.
    - `Lợi ích:` Giúp phát hiện vấn đề sớm và cải thiện khả năng sửa lỗi.
- `10. Security and Authentication`
    - `Mô tả`: Áp dụng các biện pháp bảo mật như OAuth hoặc JWT để xác thực và phân quyền truy cập.
    - `Lợi ích:` Đảm bảo an toàn thông tin khi giao tiếp giữa các service.
## 4. Vấn đề khi có 1 service làm trung gian (thường gọi là API Gateway hoặc Service Broker) và giải pháp
### **1. Vấn đề**:
- **Tải nặng**
    - `Nguyên nhân:` Tất cả các yêu cầu từ client đều phải đi qua service trung gian, dẫn đến tải nặng hơn cho service đó.
    - `Hệ quả:` Có thể gây ra độ trễ cao và làm giảm hiệu suất của hệ thống nếu không được quản lý tốt.
- **Điểm nghẽn**
    - `Nguyên nhân:` Nếu service trung gian không đủ mạnh để xử lý lưu lượng lớn, nó có thể trở thành điểm nghẽn trong kiến trúc.
    - `Hệ quả:` Có thể gây ra sự gián đoạn hoặc làm giảm khả năng sẵn sàng của toàn bộ hệ thống.
- **Thách thức về Scalable**
    - `Nguyên nhân:` Để cải thiện khả năng mở rộng, cần phải thiết lập nhiều instance của service trung gian.
    - `Hệ quả:` Quản lý và cân bằng tải giữa các instance có thể phức tạp.

### **2. Giải pháp**
- **Cân bằng tải:** Sử dụng một bộ cân bằng tải để phân phối yêu cầu đến nhiều instance của service trung gian.
- **Sử dụng cache:** Giảm tải bằng cách cache các yêu cầu thường gặp, làm giảm số lượng yêu cầu cần phải xử lý.
- **Tối ưu hóa hiệu suất:** Thực hiện tối ưu hóa mã, cấu hình, và hạ tầng để cải thiện hiệu suất.
- **Phân tách theo chức năng:** Nếu cần, chia nhỏ service trung gian thành nhiều phần, mỗi phần xử lý các tác vụ riêng biệt.
## **5. Các điểm cần chú ý khi có 1 service làm trung gian để giao tiếp cho các service khác**
### **1. Cân bằng tải**
#### **Các loại cân bằng tải**
- `Cân bằng tải phân tán (Round Robin):` Phân phối yêu cầu đến từng server theo thứ tự.
- `Cân bằng tải có trọng số (Weighted Round Robin):` Gán trọng số cho các server dựa trên khả năng xử lý của chúng. Server mạnh hơn nhận nhiều yêu cầu hơn.
- `Cân bằng tải theo địa chỉ IP (IP Hash):` Sử dụng địa chỉ IP của client để xác định server sẽ xử lý yêu cầu nhằm duy trì sự nhất quán trong phiên làm việc.
- `Cân bằng tải theo yêu cầu (Least Connections):` Chọn server hiện đang có ít kết nối nhất để xử lý yêu cầu mới.
#### **Phương pháp thực hiện cân bằng tải**
- `Sử dụng Load Balancer phần cứng:`
Thiết bị phần cứng chuyên dụng như F5 hoặc Citrix ADC có thể tự động phân phối lưu lượng.
- `Sử dụng Load Balancer phần mềm:`
Các ứng dụng như NGINX, HAProxy, hoặc Traefik có thể cấu hình để làm cân bằng tải cho các server.
- `Cân bằng tải trong Cloud:`
Các dịch vụ như Amazon Elastic Load Balancing (ELB) hoặc Google Cloud Load Balancing cung cấp chức năng cân bằng tải mà không cần triển khai phần cứng.

#### **Một số thông số phổ biến để theo dỗi cân bằng tải**
- `CPU Usage`
    - `Mô tả:` Mức sử dụng CPU cho biết bao nhiêu tài nguyên CPU đang được tiêu thụ bởi dịch vụ.
    - `Tại sao quan trọng:` Sử dụng nhiều CPU có thể chỉ ra rằng dịch vụ đang xử lý nhiều yêu cầu hoặc có vấn đề hiệu suất.
- `Memory Usage`
    - `Mô tả:` Mức sử dụng bộ nhớ cho biết bao nhiêu RAM đang được tiêu thụ.
    - `Tại sao quan trọng:` Sử dụng bộ nhớ cao có thể dẫn đến giảm hiệu suất hoặc crash nếu vượt quá giới hạn.
- `Network I/O`
    - `Mô tả:` Lưu lượng truy cập mạng vào và ra từ dịch vụ.
    - `Tại sao quan trọng:` Nâng cao lưu lượng truy cập có thể chỉ ra rằng dịch vụ đang nhận hoặc gửi dữ liệu nhiều hơn bình thường.
- `Disk I/O`
    - `Mô tả:` Tần suất và lưu lượng truy cập vào ổ đĩa.
    - `Tại sao quan trọng:` Nếu dịch vụ thường xuyên truy cập vào đĩa, có thể gây ra độ trễ và ảnh hưởng đến hiệu suất.
- `Request Rate`
    - `Mô tả:` Số lượng yêu cầu đến dịch vụ trong một khoảng thời gian nhất định.
    - `Tại sao quan trọng:` Tăng số lượng yêu cầu có thể dẫn đến tải cao và cần cân bằng tải hợp lý.
- `Error Rate`
    - `Mô tả:` Tỷ lệ yêu cầu thất bại so với tổng số yêu cầu.
    - `Tại sao quan trọng:` Tăng cao lỗi có thể là dấu hiệu của vấn đề trong dịch vụ hoặc dấu hiệu quá tải.
- `Response Time`
    - `Mô tả:` Thời gian mà dịch vụ cần để xử lý yêu cầu và trả về phản hồi.
    - `Tại sao quan trọng:` Thời gian phản hồi lâu có thể chỉ ra rằng dịch vụ đang gặp vấn đề về hiệu suất.
- `Active Connections`
Mô tả: Số kết nối đang hoạt động tại thời điểm hiện tại.
    - `Tại sao quan trọng:` Số lượng kết nối cao có thể chỉ ra rằng dịch vụ đang xử lý nhiều yêu cầu đồng thời.
#### **Ví dụ cài đặt với NGINX**
```nginx
http {
    upstream backend {
        server backend1.example.com;
        server backend2.example.com;
        server backend3.example.com;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend;
        }
    }
}
```
#### **Lợi ích của cân bằng tải**
- `Tăng cường tính sẵn sàng:` Nếu một server bị lỗi, yêu cầu sẽ tự động được chuyển sang server khác.
- `Tối ưu hóa hiệu suất:` Phân phối tải giúp giảm độ trễ và cải thiện trải nghiệm người dùng.
- `Mở rộng dễ dàng:` Có thể thêm hoặc loại bỏ server mà không làm gián đoạn dịch vụ.
### **2. Sử dụng Cache trong Kiến trúc Microservices**
> Cache là một phương pháp hiệu quả giúp cải thiện hiệu suất ứng dụng bằng cách lưu trữ tạm thời dữ liệu, giảm thiểu số lần yêu cầu đến server và giảm độ trễ trong việc truy cập dữ liệu. Dưới đây là một số giải pháp và phương pháp sử dụng cache trong kiến trúc microservices.
#### **Loại Cache**
- `In-Memory Cache:` Lưu trữ dữ liệu trong bộ nhớ RAM để truy cập nhanh chóng. Các giải pháp phổ biến bao gồm:
    - `Redis:` Cung cấp tốc độ nhanh, hỗ trợ các kiểu dữ liệu phong phú và khả năng mở rộng.
    - `Memcached:` Một hệ thống cache đơn giản, hiệu suất cao nhưng với kiểu dữ liệu hạn chế.
- `Distributed Cache:` Chia sẻ cache giữa nhiều instances của dịch vụ để đảm bảo tính nhất quán và sẵn sàng khi có sự cố.
#### **Chiến lược Cache**
- `Cache Aside`: Dịch vụ kiểm tra cache trước khi truy vấn cơ sở dữ liệu. Nếu dữ liệu không có trong cache, nó sẽ truy vấn cơ sở dữ liệu và sau đó lưu trữ kết quả vào cache.
- `Write Through`: Khi ứng dụng ghi dữ liệu, nó sẽ đồng thời ghi vào cache và cơ sở dữ liệu. Điều này giúp đảm bảo rằng cache luôn cập nhật thông tin mới nhất.
- `Write Back`: Ứng dụng ghi dữ liệu vào cache trước, và sau đó mới ghi vào cơ sở dữ liệu. Giải pháp này cải thiện tốc độ nhưng có nguy cơ mất dữ liệu nếu cache gặp sự cố.

#### **Giải pháp Caching**
- `Cấu hình Cache Header:` Tối ưu hóa trình duyệt client bằng cách sử dụng các cache header như Expires, Cache-Control.
- `Tạo Key phù hợp`: Sử dụng khóa cache chính xác cho từng loại dữ liệu để tránh xung đột và nhầm lẫn.
#### **Thời gian sống (TTL) của Cache**
 - `Thiết lập TTL:` Cấu hình thời gian sống cho dữ liệu trong cache để tự động xóa hoặc làm mới dữ liệu khi hết hạn.
#### **Giám sát Cache**
- `Theo dõi hiệu suất:` Sử dụng các công cụ giám sát như Prometheus để theo dõi hiệu suất cache, xác định tỷ lệ hit/miss.
#### **Cách Triển khai Cache**
> Dưới đây là một ví dụ đơn giản về cách sử dụng Redis trong ứng dụng Node.js:

```javascript
const redis = require('redis');
const client = redis.createClient();

function getData(key) {
    return new Promise((resolve, reject) => {
        client.get(key, (err, data) => {
            if (data) {
                return resolve(JSON.parse(data));
            } else {
                // Lấy dữ liệu từ cơ sở dữ liệu
                const dbData = fetchFromDatabase(key);
                client.setex(key, 3600, JSON.stringify(dbData)); // Cache dữ liệu trong 1 giờ
                return resolve(dbData);
            }
        });
    });
}
```

>Sử dụng thư viện redis-py để kết nối và làm việc với Redis.
```python
import redis
import json

# Kết nối đến Redis
client = redis.StrictRedis(host='localhost', port=6379, db=0)

def get_data(key):
    # Kiểm tra dữ liệu trong cache
    cached_data = client.get(key)
    
    if cached_data:
        return json.loads(cached_data)  # Trả lại dữ liệu đã cache
    else:
        # Giả lập truy vấn cơ sở dữ liệu
        db_data = fetch_from_database(key)
        client.setex(key, 3600, json.dumps(db_data))  # Cache dữ liệu trong 1 giờ
        return db_data

def fetch_from_database(key):
    # Giả lập hàm truy vấn cơ sở dữ liệu
    return {"key": key, "value": "data from database"}  # Dữ liệu mẫu

# Sử dụng hàm
data = get_data('my_key')
print(data)
```
> Trong Java, bạn có thể sử dụng thư viện Jedis để làm việc với Redis.
```java
import redis.clients.jedis.Jedis;

public class RedisCacheExample {
    public static void main(String[] args) {
        Jedis jedis = new Jedis("localhost", 6379);
        
        String key = "my_key";
        String cachedData = jedis.get(key);
        
        if (cachedData != null) {
            System.out.println("Data from cache: " + cachedData);
        } else {
            // Giả lập truy vấn cơ sở dữ liệu
            String dbData = fetchFromDatabase(key);
            jedis.setex(key, 3600, dbData);  // Cache dữ liệu trong 1 giờ
            System.out.println("Data from database: " + dbData);
        }
        
        jedis.close();
    }
    
    private static String fetchFromDatabase(String key) {
        // Giả lập hàm truy vấn cơ sở dữ liệu
        return "{\"key\":\"" + key + "\",\"value\":\"data from database\"}";  // Dữ liệu mẫu
    }
}
```