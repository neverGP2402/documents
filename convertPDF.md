# Logic Convert PDF

## Yêu cầu hệ thống
- Khi user upload file DOC/DOCX thì hệ thống sẽ convert sang PDF ngay lập tức để user preview và kiểm tra nội dung trước khi ký số.
- File PDF sau đó sẽ là file chính thức để ký nên cần đảm bảo layout không sai lệch so với file Word.

## Flow hệ thống

```
User upload DOC/DOCX
        ↓
Server convert DOCX → PDF
        ↓
User preview PDF
        ↓
User ký số
```

## Các option khác

### 1. Dùng Cloud API để convert file DOCX -> PDF (ConvertApi, CloudConvert, Cloudmersive Document Conversion API, GroupDocs.Conversion Cloud) - server side

**Ưu điểm:**
- Không cần cài đặt phần mềm
- Dễ dàng tích hợp với hệ thống
- Xử lý ngay ở Client 
- Layout giữ độ chính xác cao và gần giống với file Word gốc.

**Nhược điểm:**
- Cần có API key
- Có thể bị giới hạn số lần convert
- Phụ thuộc vào bên thứ 3
- Có thể mất phí hoặc phụ thuộc vào gói dịch vụ.

### 2. Dùng library JavaScript để convert file DOCX -> PDF (Mammoth.js, docx-preview, jsPDF, html2pdf.js) - client side

**Ưu điểm:**
- Không cần cài đặt phần mềm
- Dễ dàng tích hợp với hệ thống
- Xử lý ngay ở Client 
- Miễn phí

**Nhược điểm:**
- Độ chính xác thấp
- Đa phần phải tự xử lý layout vì flow doc -> Parse DOCX -> HTML -> PDF => Dễ bị sai lệch
- Phụ thuộc vào RAM và CPU của client => Có thể gây lag
- Bảo mật dữ liệu có thể bị ảnh hưởng

### 3. Convert bằng các thư viện thương mại (Aspose.Words, GroupDocs Conversion) - server side

**Ưu điểm:**
- Layout giữ độ chính xác cao và gần giống với file Word gốc.
- Hỗ trợ nhiều định dạng file
- Dễ dàng tích hợp với hệ thống
- Bảo mật dữ liệu tốt

**Nhược điểm:**
- Cần có license
- Chi phí license cao
- Phụ thuộc vào bên thứ 3

### 4. Convert bằng các Office engine (Microsoft Word, LibreOffice) - server side => Đề xuất

**Ưu điểm:**
- Layout giữ độ chính xác cao và gần giống với file Word gốc.
- Hỗ trợ nhiều định dạng file
- Dễ dàng tích hợp với hệ thống
- Bảo mật dữ liệu tốt

**Nhược điểm:**
- Cần tải application Office (Microsoft Word - windows, LibreOffice/Soffice - windows/linux)
- Đối với Soffice (linux): cần cài thêm font riêng

## Đề xuất hiện tại
- Sử dụng Soffice để convert DOCX -> PDF (convert ở server side)
- LibreOffice là một bộ phần mềm office mã nguồn mở tương tự Microsoft Office, có thể chạy convert document thông qua CLI (soffice).

**Ưu điểm:**
- Miễn phí
- Layout giữ độ chính xác cao và gần giống với file Word gốc.
- Dễ dàng tích hợp với hệ thống
- Hỗ trợ nhiều định dạng file
- Có thể chạy trên cả linux và windows server

**Nhược điểm:**
- Cần cài đặt thêm phần mềm ở server
- Tải font từng font riêng 

---

> **Kết luận:** 
- Sau khi so sánh các giải pháp thì Office Engine (LibreOffice) là giải pháp phù hợp nhất cho hệ thống hiện tại. 
- Do file PDF sẽ được dùng để ký số nên độ chính xác layout là yếu tố quan trọng nhất. 
- Vì vậy giải pháp sử dụng Office Engine (LibreOffice) là phù hợp nhất. 
- Ngoài ra cần đảm bảo server có đầy đủ font được sử dụng trong file Word để tránh sai lệch layout khi convert.
