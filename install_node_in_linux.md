# Cài đặt công cụ n để quản lý phiên bản Node.js
- Một trong những cách tốt nhất để cài đặt phiên bản cụ thể của Node.js là sử dụng n, một công cụ quản lý Node.js phiên bản. Trước tiên, hãy cài đặt n thông qua npm (trình quản lý gói của Node.js).

- Đầu tiên, cài đặt các yêu cầu cơ bản:
```bash
sudo dnf install -y gcc-c++ make
```
Cài đặt Node.js mặc định để sử dụng npm (bạn có thể gỡ bỏ sau khi cài đặt n):

```bash
sudo dnf module enable nodejs:16
sudo dnf install -y nodejs
```
3. Cài đặt n qua npm
Sau khi Node.js được cài đặt, bạn có thể sử dụng npm để cài đặt n:

```bash
sudo npm install -g n
```
4. Cài đặt Node.js phiên bản 16.14.2
Sau khi cài đặt n, bạn có thể sử dụng nó để cài đặt Node.js phiên bản 16.14.2:

```bash
sudo n 16.14.2
```
5. Kiểm tra phiên bản Node.js
Sau khi cài đặt xong, kiểm tra phiên bản Node.js:

```bash
node -v
```

6. Xóa Node.js mặc định (tuỳ chọn)
Nếu bạn không cần phiên bản Node.js mặc định đã cài qua dnf, bạn có thể gỡ cài đặt nó:

```bash
sudo dnf remove nodejs
```
Lỗi "missing groups or modules" xuất hiện khi hệ thống không tìm thấy module nodejs:16 trong kho lưu trữ. Điều này có thể là do phiên bản Node.js không có sẵn trong kho mặc định của AlmaLinux 9.

Bạn có thể cài đặt Node.js 16.14.2 theo một cách khác, đó là sử dụng NodeSource - một nguồn cung cấp kho lưu trữ Node.js phổ biến. Dưới đây là cách thực hiện:

1. Thêm kho lưu trữ NodeSource
NodeSource cung cấp các phiên bản khác nhau của Node.js cho các hệ thống dựa trên RHEL/CentOS (bao gồm AlmaLinux).

Chạy lệnh sau để thêm kho Node.js 16.x từ NodeSource:

```bash
curl -fsSL https://rpm.nodesource.com/setup_16.x | sudo bash -
```
Lệnh này sẽ cấu hình kho lưu trữ NodeSource trên hệ thống của bạn.

2. Cài đặt Node.js 16
Sau khi thêm kho NodeSource, bạn có thể cài đặt Node.js 16.14.2 bằng lệnh:

```bash
sudo dnf install -y nodejs
```
3. Kiểm tra phiên bản Node.js
Sau khi cài đặt xong, kiểm tra phiên bản Node.js để đảm bảo bạn đã cài đặt đúng:

```bash
node -v
```

4. Cài đặt các công cụ bổ sung
Nếu bạn cần các công cụ phát triển (ví dụ, gcc, g++), bạn có thể cài đặt chúng bằng lệnh sau:

```bash
sudo dnf groupinstall 'Development Tools'
```