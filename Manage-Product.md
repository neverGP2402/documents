# Phần mềm "Quản lý con hàng điện tử"

### I. TỔNG QUAN
Phần mềm được xây dựng trên nền tản mobile app và sử dụng React Native để triển khai ứng dụng giúp quản lý thông tin các con hàng điện tử. Phần mềm sẽ không kết nối với Database để quản lý dữ liệu thay vào đó là quản lý dữ liệu bằng file json khi chỉnh sửa dữ liệu sẽ chỉnh sửa trên file đó

### II. NGHIỆP VỤ VÀ MÀN HÌNH

#### 1. Quản lý thông tin con hàng:
- Mã con hàng
- Tên con hàng
- Hình ảnh (upload hoặc chụp)
- Số cổng (lỗ) kết nối

#### 1. Quản lý thông tin con hàng:
- Mã con hàng
- Tên con hàng
- Hình ảnh (upload hoặc chụp)
- Số cổng (lỗ) kết nối
#### 2. Quản lý thông tin dây kết nối
- Tên (loại) dây
- Màu (chọn từ option 7 màu cầu vòng mã màu RGB)
#### 3. Cấu hình cổng kết nối
- Bước 1 Chọn con hàng  
- Bước 2 Cấu hình cổng kết nối cho con hàng (Chọn dây cho cổng)

#### 4. Màn hình tra hiển thị danh sách con hàng
Gồm: tên con hàng, hình ảnh (dạng avt click vào popup lên xem review), cổng kết nối theo dây (Dây nào màu đó nếu không chưa cấu hình hoặc k có đánh dấu x)

## III. CẤU TRÚC DỮ LIỆU
> Dữ liệu chia thành đối tượng và mỗi đối tượng là 1 file
#### Thông tin con hàng (product.json):
``` json
{
    "id": "id",
    "name": "Product Name",
    "code": " Product code",
    "total_port_connect": "Total Port Connections",
    "image_path": "images/hinh_01.jpg",
    "description": "Mô tả",
    "data_connect": [
        {
            "port": 1,
            "id_wire": "id dây"
        },
        {
            "port": 2,
            "id_wire": "id dây"
        },
        {
            "port": 3,
            "id_wire": null
        },
    ]
}
```

#### Thông tin dây kết nối (wire.json):
``` json
[
    {
        "id": 1,
        "name": "Dây 1",
        "color": "green",
    },
    {
        "id": 2,
        "name": "Dây 2",
        "color": "red",
    },
    {
        "id": 3,
        "name": "Dây 3",
        "color": "blue",
    },
    //  Các dây khác
]
```

## IV CÁC MODULE CẦN
1. Module cho product.json (productModule.js): Cung cấp các chức năng thêm, sửa và xóa đối tượng con hàng từ file product.json.

``` javascript
const fs = require('fs');
const path = require('path');

const productFilePath = path.join(__dirname, 'product.json');

// Đọc file JSON
const readProductData = () => {
  try {
    const data = fs.readFileSync(productFilePath, 'utf8');
    return JSON.parse(data);
  } catch (err) {
    throw new Error('Lỗi đọc file product.json: ' + err.message);
  }
};

// Ghi dữ liệu vào file JSON
const writeProductData = (data) => {
  try {
    fs.writeFileSync(productFilePath, JSON.stringify(data, null, 2), 'utf8');
  } catch (err) {
    throw new Error('Lỗi ghi file product.json: ' + err.message);
  }
};

// Thêm một sản phẩm mới
const addProduct = (newProduct) => {
  try {
    const products = readProductData();
    products.push(newProduct);
    writeProductData(products);
    return { status: 'success', data: 'Sản phẩm đã được thêm.' };
  } catch (err) {
    return { status: 'error', data: err.message };
  }
};

// Sửa thông tin sản phẩm theo ID
const editProduct = (id, updatedProduct) => {
  try {
    const products = readProductData();
    const index = products.findIndex(product => product.id === id);
    
    if (index !== -1) {
      products[index] = { ...products[index], ...updatedProduct };
      writeProductData(products);
      return { status: 'success', data: 'Sản phẩm đã được cập nhật.' };
    } else {
      return { status: 'error', data: 'Không tìm thấy sản phẩm với ID này.' };
    }
  } catch (err) {
    return { status: 'error', data: err.message };
  }
};

// Xóa sản phẩm theo ID
const deleteProduct = (id) => {
  try {
    const products = readProductData();
    const updatedProducts = products.filter(product => product.id !== id);

    if (updatedProducts.length < products.length) {
      writeProductData(updatedProducts);
      return { status: 'success', data: 'Sản phẩm đã được xóa.' };
    } else {
      return { status: 'error', data: 'Không tìm thấy sản phẩm với ID này.' };
    }
  } catch (err) {
    return { status: 'error', data: err.message };
  }
};

module.exports = { addProduct, editProduct, deleteProduct };

```

2. Module cho wire.json (wireModule.js)
```javascript
const fs = require('fs');
const path = require('path');

const wireFilePath = path.join(__dirname, 'wire.json');

// Đọc file JSON
const readWireData = () => {
  try {
    const data = fs.readFileSync(wireFilePath, 'utf8');
    return JSON.parse(data);
  } catch (err) {
    throw new Error('Lỗi đọc file wire.json: ' + err.message);
  }
};

// Ghi dữ liệu vào file JSON
const writeWireData = (data) => {
  try {
    fs.writeFileSync(wireFilePath, JSON.stringify(data, null, 2), 'utf8');
  } catch (err) {
    throw new Error('Lỗi ghi file wire.json: ' + err.message);
  }
};

// Thêm một dây mới
const addWire = (newWire) => {
  try {
    const wires = readWireData();
    wires.push(newWire);
    writeWireData(wires);
    return { status: 'success', data: 'Dây đã được thêm.' };
  } catch (err) {
    return { status: 'error', data: err.message };
  }
};

// Sửa thông tin dây theo ID
const editWire = (id, updatedWire) => {
  try {
    const wires = readWireData();
    const index = wires.findIndex(wire => wire.id === id);

    if (index !== -1) {
      wires[index] = { ...wires[index], ...updatedWire };
      writeWireData(wires);
      return { status: 'success', data: 'Dây đã được cập nhật.' };
    } else {
      return { status: 'error', data: 'Không tìm thấy dây với ID này.' };
    }
  } catch (err) {
    return { status: 'error', data: err.message };
  }
};

// Xóa dây theo ID
const deleteWire = (id) => {
  try {
    const wires = readWireData();
    const updatedWires = wires.filter(wire => wire.id !== id);

    if (updatedWires.length < wires.length) {
      writeWireData(updatedWires);
      return { status: 'success', data: 'Dây đã được xóa.' };
    } else {
      return { status: 'error', data: 'Không tìm thấy dây với ID này.' };
    }
  } catch (err) {
    return { status: 'error', data: err.message };
  }
};

module.exports = { addWire, editWire, deleteWire };
```
3. Ví dụ về cách sử dụng các module (sử dụng hàm và xử lý kết quả)

``` javascript
const { addProduct, editProduct, deleteProduct } = require('./productModule');
const { addWire, editWire, deleteWire } = require('./wireModule');

// Thêm sản phẩm
const newProduct = {
  "id": "id_123",
  "name": "Product Name",
  "code": "Product Code",
  "total_port_connect": 5,
  "image_path": "images/hinh_01.jpg",
  "description": "Mô tả chi tiết về sản phẩm",
  "data_connect": [
    { "port": 1, "id_wire": 1 },
    { "port": 2, "id_wire": 2 },
    { "port": 3, "id_wire": null }
  ]
};

const addProductResult = addProduct(newProduct);
console.log(addProductResult.status, addProductResult.data);

// Sửa sản phẩm
const updatedProduct = {
  "name": "Updated Product Name",
  "description": "Updated description"
};
const editProductResult = editProduct("id_123", updatedProduct);
console.log(editProductResult.status, editProductResult.data);

// Xóa sản phẩm
const deleteProductResult = deleteProduct("id_123");
console.log(deleteProductResult.status, deleteProductResult.data);

// Thêm dây
const newWire = { "id": 4, "name": "Dây 4", "color": "yellow" };
const addWireResult = addWire(newWire);
console.log(addWireResult.status, addWireResult.data);

// Sửa dây
const updatedWire = { "name": "Dây 4 - New Name", "color": "orange" };
const editWireResult = editWire(4, updatedWire);
console.log(editWireResult.status, editWireResult.data);

// Xóa dây
const deleteWireResult = deleteWire(4);
console.log(deleteWireResult.status, deleteWireResult.data);
```

4. Module upload và xóa hình ảnh (imageModule.js)
```javascript
const fs = require('fs');
const path = require('path');

// Thư mục lưu trữ ảnh
const imageDirectory = path.join(__dirname, 'images');

// Kiểm tra và tạo thư mục nếu chưa tồn tại
if (!fs.existsSync(imageDirectory)) {
  fs.mkdirSync(imageDirectory);
}

// Hàm upload hình ảnh (base64 và tên ảnh)
const uploadImage = (base64Data, fileName) => {
  try {
    // Tạo đường dẫn lưu tệp ảnh
    const filePath = path.join(imageDirectory, fileName);

    // Lọc base64 để lấy phần dữ liệu ảnh sau dấu phẩy
    const base64 = base64Data.split(',')[1];

    // Chuyển đổi base64 thành buffer
    const buffer = Buffer.from(base64, 'base64');

    // Ghi buffer vào tệp
    fs.writeFileSync(filePath, buffer);
    return { status: 'success', data: `Hình ảnh ${fileName} đã được tải lên.` };
  } catch (err) {
    return { status: 'error', data: `Lỗi tải ảnh lên: ${err.message}` };
  }
};

// Hàm xóa hình ảnh theo tên file
const deleteImage = (fileName) => {
  try {
    const filePath = path.join(imageDirectory, fileName);

    // Kiểm tra nếu file tồn tại
    if (fs.existsSync(filePath)) {
      fs.unlinkSync(filePath);
      return { status: 'success', data: `Hình ảnh ${fileName} đã được xóa.` };
    } else {
      return { status: 'error', data: `Không tìm thấy hình ảnh với tên ${fileName}.` };
    }
  } catch (err) {
    return { status: 'error', data: `Lỗi xóa ảnh: ${err.message}` };
  }
};

module.exports = { uploadImage, deleteImage };
```