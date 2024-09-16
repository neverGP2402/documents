# 1. Cài đặt Python từ kho EPEL (Extra Packages for Enterprise Linux)
### Trước tiên, cần thêm kho lưu trữ EPEL (Extra Packages for Enterprise Linux), vì Python 3.9 có thể không có sẵn trong kho mặc định của AlmaLinux 9.

Bước 1: Cài đặt kho EPEL
Chạy lệnh sau để thêm kho EPEL:


```bash
sudo dnf install -y epel-release
```
Bước 2: Cài đặt Python 3.9
Sau khi thêm kho EPEL, bạn có thể cài đặt Python 3.9 bằng lệnh:

```bash
sudo dnf install -y python39
```
## 2. Kiểm tra phiên bản Python 3.9
Sau khi cài đặt xong, kiểm tra phiên bản Python để đảm bảo rằng Python 3.9 đã được cài đặt thành công:

```bash
python3.9 --version
```
## 3. Thiết lập Python 3.9 làm phiên bản mặc định (tuỳ chọn)
Nếu bạn muốn thiết lập Python 3.9 làm phiên bản mặc định trên hệ thống, hãy thay đổi liên kết python3 đến Python 3.9 bằng cách:

```bash
sudo alternatives --set python3 /usr/bin/python3.9
```
## 4. Cài đặt pip cho Python 3.9
Pip là trình quản lý gói cho Python, có thể không được cài đặt tự động. Bạn có thể cài đặt pip bằng lệnh sau:

```bash
sudo dnf install -y python39-pip
```


## Lỗi "No match for argument" xảy ra do gói python39-pip không có sẵn trong kho lưu trữ mặc định của AlmaLinux 9. Dưới đây là cách khác để cài đặt pip cho Python 3.9.

## 1. Cài đặt Python 3.9 trước (nếu chưa)
Nếu bạn chưa cài đặt Python 3.9, hãy đảm bảo Python 3.9 đã được cài đặt bằng lệnh sau:

```bash
sudo dnf install -y python39
```
2. Cài đặt pip thủ công bằng get-pip.py
Nếu python39-pip không có sẵn trong kho, bạn có thể cài đặt pip cho Python 3.9 bằng cách tải xuống và sử dụng script get-pip.py.

Bước 1: Tải xuống script get-pip.py
Chạy lệnh sau để tải xuống script get-pip.py:

```bash
curl -O https://bootstrap.pypa.io/get-pip.py
```
Bước 2: Cài đặt pip bằng Python 3.9
Chạy lệnh sau để cài đặt pip cho Python 3.9:

```bash
python3.9 get-pip.py
```
3. Kiểm tra phiên bản pip
Sau khi cài đặt thành công, kiểm tra phiên bản pip:

```bash
pip3.9 --version
```
4. Xóa script get-pip.py (tuỳ chọn)
Sau khi hoàn tất cài đặt pip, bạn có thể xóa script get-pip.py nếu không cần dùng nữa:

```bash
rm get-pip.py
```