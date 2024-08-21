# Over view
## 1. Message broker là gì?
- `Doc`: Message broker (trình môi giới thông điệp) là một thành phần phần mềm được sử dụng trong các hệ thống nhắn tin để tạo điều kiện giao tiếp giữa các ứng dụng, hệ thống hoặc dịch vụ khác nhau. Nó hoạt động như một trung gian, cho phép các thành phần này trao đổi thông tin bằng cách gửi và nhận thông điệp. Vai trò chính của một message broker là quản lý việc định tuyến thông điệp giữa nhà sản xuất (producer - bên gửi thông điệp) và người tiêu dùng (consumer - bên nhận thông điệp), đảm bảo rằng thông điệp được giao đúng cách và theo thứ tự.
- `Me`: Message broker được hiểu như là 1 trung gian chịu trách nhiệm giao tiếp và truyền tải message/data giữa các đối tượng (Nhận và gửi)
## 2. Đặt điểm và lợi ích:
- `Giảm phụ thuộc (Decoupling)`: Message broker giúp giảm sự phụ thuộc giữa các thành phần của hệ thống, cho phép chúng hoạt động độc lập và theo nhịp độ riêng. Điều này giúp hệ thống dễ mở rộng và bảo trì hơn.

- `Độ tin cậy (Reliability)`: Message broker đảm bảo rằng thông điệp được giao một cách tin cậy, ngay cả khi có sự cố mạng hoặc hệ thống. Thường có các cơ chế như lưu trữ thông điệp (message persistence) và xác nhận (acknowledgment) để đảm bảo giao hàng.

- `Định tuyến thông điệp (Message Routing)`: Message broker có thể định tuyến thông điệp dựa trên các quy tắc cụ thể, chẳng hạn như nội dung của thông điệp hoặc loại sự kiện. Điều này cho phép các mô hình giao tiếp linh hoạt.

- `Cân bằng tải (Load Balancing)`: Nó có thể phân phối thông điệp cho nhiều người tiêu dùng để cân bằng tải và cải thiện hiệu suất.

- `Chuyển đổi giao thức (Protocol Translation)`: Một số message broker có thể chuyển đổi giữa các giao thức nhắn tin khác nhau, cho phép giao tiếp giữa các hệ thống sử dụng các công nghệ khác nhau. 
- `Tóm tắt`: Linh hoạt cho việc bảo trì và mở rộng, đảm bảo dữ liệu dữ liệu/message được giao tiếp/lưu trữ ngay khi gặp sự cố về hệ thống hoặc mạng (vì message broker sẽ lưu lại dữ liệu nhận và xử lý khi cần), giao tiếp linh hoạt có thể gửi và nhận cho 1 nhóm hoặc 1 đối tượng cụ thể (routing), cân bằng tải cho hệ thống giúp phân bổ request hoặc tối ưu hóa tài nguyên đảm bảo hiệu suất được cân bằng giữa các hệ thống và cuối cùng là cho phép giao tiếp giữa các công nghệ khác nhau ví dụ như: có thể sử dụng giao tiếp giữa 2 ngôn ngữ lập trình hoặc 2 framework khác nhau
## Câu hỏi:
>1. So sánh Socket.io và Message Broker: 
- `Socket.IO` là một lựa chọn tuyệt vời cho các ứng dụng web thời gian thực, nơi bạn cần giao tiếp hai chiều và liên tục giữa máy khách và máy chủ.
- `Message Broker` lại mạnh mẽ hơn trong việc quản lý truyền thông điệp giữa các dịch vụ trong một hệ thống phân tán hoặc microservices, với các tính năng nâng cao về định tuyến, độ tin cậy, và cân bằng tải.
>2. Các message broker phổ biến hiện nay:
- `Apache Kafka`:
Được thiết kế để xử lý lượng lớn dữ liệu trên nhiều máy chủ.
Thích hợp cho việc truyền thông tin theo thời gian thực và phân tích dữ liệu.
+ `RabbitMQ`:
Dựa trên mô hình hàng đợi tin nhắn.
Hỗ trợ nhiều giao thức khác nhau và dễ dàng mở rộng.
- `ActiveMQ`:
Một message broker mã nguồn mở cung cấp hỗ trợ cho JMS (Java Message Service).
Hỗ trợ nhiều giao thức và có tính năng độ tin cậy cao.
- `Redis`:
Dùng chủ yếu như một kho lưu trữ dữ liệu trong bộ nhớ nhưng cũng hỗ trợ publish/subscribe.
Có tốc độ rất nhanh và dễ sử dụng.
- `NATS`:
Một message broker nhẹ, nhanh, chuyên dụng cho microservices.
Hỗ trợ các mô hình publish/subscribe và request/reply.
- `Amazon SQS`:
Dịch vụ hàng đợi tin nhắn được quản lý bởi AWS.
Đảm bảo độ tin cậy cao với khả năng mở rộng linh hoạt.
- `Google Pub/Sub`:
Dịch vụ của Google Cloud cho việc trao đổi tin nhắn giữa các ứng dụng.
Hỗ trợ xử lý tin nhắn theo thời gian thực và khả năng mở rộng tốt.
> 1. Socket.io giống vậy nó có phải là 1 message broker không?
- `1. Socket.IO`
Giao tiếp thời gian thực: Socket.IO chủ yếu được sử dụng để thiết lập kết nối WebSocket, giúp truyền dữ liệu giữa máy chủ và khách hàng trong thời gian thực.
Mô hình sự kiện: Dựa trên mô hình sự kiện, cho phép gửi và nhận thông điệp trực tiếp giữa client và server.
Đơn giản hóa: Tập trung vào việc xây dựng ứng dụng web và di động cần giao tiếp thời gian thực.
- `2. Message Broker`
Quản lý tin nhắn: Được thiết kế để quản lý và phân phối tin nhắn giữa các ứng dụng hoặc dịch vụ, thường trong môi trường phân tán.
Độ bền: Hỗ trợ lưu trữ và quản lý độ tin cậy của tin nhắn đến khi được tiêu thụ.
Mô hình phức tạp: Thường hỗ trợ nhiều mô hình giao tiếp như pub/sub, queue, và hơn thế nữa.
>4. Message broker có phân loại không. Nếu có thì gồm những loại nào?

- **1. Theo Mô Hình Giao Tiếp**
  - **`Queue-based`: Tin nhắn được gửi vào hàng đợi và được tiêu thụ bởi một hoặc nhiều người tiêu dùng. Ví dụ: RabbitMQ, ActiveMQ.**
  - **`Publish/Subscribe`: Nhà xuất bản phát tin nhắn đến nhiều người đăng ký, cho phép nhiều người tiêu dùng nhận thông điệp cùng lúc. Ví dụ: Apache Kafka, NATS.**
- **2. Theo Kiến Trúc**
  - **`Centralized`: Một broker duy nhất quản lý toàn bộ việc giao tiếp. Điều này đơn giản hóa quản lý nhưng có thể tạo ra điểm nghẽn.**
  - **`Distributed`Nhiều broker làm việc cùng nhau để phân phối tải, cung cấp độ tin cậy và khả năng mở rộng cao hơn.**
- **3. Theo Tính Năng**
  - **`Độ Bền`: Một số broker lưu trữ tin nhắn cho đến khi chúng được tiêu thụ, trong khi những cái khác không đảm bảo lưu trữ.**
  - **`Khả Năng Mở Rộng`: Một số broker dễ mở rộng bằng cách thêm các nút mới, trong khi những cái khác khó khăn hơn.**
- **4. Theo Ngôn Ngữ và Giao Thức**
  - **`Giao Thức Nhất Định`: Một số broker chỉ hỗ trợ các giao thức như AMQP, MQTT, hay STOMP.**
  - **`Đa Giao Thức`: Hỗ trợ nhiều giao thức khác nhau để tương tác với các ứng dụng đa dạng.**
## Giao thức:
> 1. Các loại giao thức:
Có rất nhiều giao thức được sử dụng trong các message broker, dưới đây là một số giao thức phổ biến:

- `1. AMQP (Advanced Message Queuing Protocol)`
Được thiết kế cho các hệ thống phân tán, hỗ trợ tính năng độ tin cậy cao, tính năng hàng đợi và pub/sub.
- `2. MQTT (Message Queuing Telemetry Transport)`
Nhẹ, thích hợp cho các ứng dụng IoT (Internet of Things), cho phép truyền tin nhắn qua các mạng không ổn định.
- `3. STOMP (Simple Text Oriented Messaging Protocol)`
Giao thức đơn giản, dựa trên văn bản, hỗ trợ giao tiếp giữa client và server.
- `4. JMS (Java Message Service)`
Giao thức chuẩn cho Java, cho phép các ứng dụng Java giao tiếp qua tin nhắn qua nhiều broker khác nhau.
- `5. XMPP (Extensible Messaging and Presence Protocol)`
Chủ yếu được sử dụng cho giao tiếp thời gian thực, như chat, nhưng cũng có thể dùng trong messaging.
- `6. HTTP/HTTPS`
Một số message broker hỗ trợ giao thức HTTP/HTTPS để gửi và nhận tin nhắn qua web.
- `7. WebSocket`
Giúp thiết lập kết nối hai chiều giữa client và server, thường được sử dụng cho truyền thông thời gian thực.
>2. Ví dụ các giao thức: Dưới đây là ví dụ cho từng giao thức message broker phổ biến:

- `1. AMQP (Advanced Message Queuing Protocol)`
Ví dụ: RabbitMQ
Một message broker phổ biến sử dụng AMQP, cho phép các ứng dụng gửi và nhận tin nhắn qua hàng đợi.
- `2. MQTT (Message Queuing Telemetry Transport)`
Ví dụ: Mosquitto
Một broker MQTT nhẹ, thường được sử dụng trong các ứng dụng IoT để truyền thông tin giữa thiết bị.
- `3. STOMP (Simple Text Oriented Messaging Protocol)`
Ví dụ: ActiveMQ
Hỗ trợ STOMP, cho phép các ứng dụng giao tiếp bằng tin nhắn theo cách đơn giản và dễ hiểu.
- `4. JMS (Java Message Service)`
Ví dụ: Apache ActiveMQ
Cung cấp API JMS để các ứng dụng Java giao tiếp qua các hệ thống message broker với nhau.
- `5. XMPP (Extensible Messaging and Presence Protocol)`
Ví dụ: ejabberd
Một server XMPP mã nguồn mở được sử dụng cho các ứng dụng chat và giao tiếp thời gian thực.
- `6. HTTP/HTTPS`
Ví dụ: Amazon SQS
Dịch vụ hàng đợi tin nhắn dựa trên HTTP, cho phép các ứng dụng gửi và nhận thông điệp qua web.
- `7. WebSocket`
Ví dụ: Socket.IO
Thư viện JavaScript cho phép giao tiếp thời gian thực giữa client và server, sử dụng WebSocket cho các kết nối hai chiều.
Mỗi giao thức và ví dụ trên đều phù hợp cho các ngữ cảnh và nhu cầu khác nhau trong việc truyền thông tin và dữ liệu.

> 3. Code example
- `1.AMQP (RabbitMQ) với Pika (Python)`

```python
import pika

# Thiết lập kết nối
connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

# Tạo hàng đợi
channel.queue_declare(queue='hello')

# Gửi tin nhắn
channel.basic_publish(exchange='', routing_key='hello', body='Hello, World!')
print(" [x] Sent 'Hello, World!'")

# Đóng kết nối
connection.close()
```

- `2. MQTT (Mosquitto) với Paho (Python)`

```python
import paho.mqtt.client as mqtt

# Callback khi kết nối thành công
def on_connect(client, userdata, flags, rc):
    print("Connected with result code " + str(rc))
    client.publish("test/topic", "Hello MQTT")

client = mqtt.Client()
client.on_connect = on_connect

# Kết nối đến broker
client.connect("localhost", 1883, 60)

# Thực hiện loop để giữ kết nối
client.loop_forever()
```
- `3. STOMP (ActiveMQ) với stomp.py (Python)`

```python
import stomp

def on_message(frame):
    print('Received message: {}'.format(frame.body))

conn = stomp.Connection([('localhost', 61613)])
conn.set_listener('', stomp.PrintingListener())
conn.connect('user', 'password', wait=True)

# Gửi tin nhắn
conn.send(body='Hello STOMP', destination='/queue/test')

# Nghe tin nhắn
conn.subscribe(destination='/queue/test', id=1, ack='auto')
```

- `4. WebSocket (Socket.IO) với Node.js`

```javascript
// server.js
const express = require('express');
const { Server } = require('socket.io');

const app = express();
const server = require('http').createServer(app);
const io = new Server(server);

io.on('connection', (socket) => {
    console.log('a user connected');
    socket.emit('message', 'Hello WebSocket');

    socket.on('disconnect', () => {
        console.log('user disconnected');
    });
});

server.listen(3000, () => {
    console.log('listening on *:3000');
});
```