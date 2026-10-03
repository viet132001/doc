# Hướng dẫn thêm dữ liệu mới

## Cấu trúc thư mục
```
data/
├── README.md
├── data_users.js          # Dữ liệu điểm bán
├── kho_nha_pp.js          # Dữ liệu kho nhà PP
└── [file_dữ_liệu_mới].js  # Các file dữ liệu khác
```

## Cách thêm dữ liệu mới

### 1. Tạo file dữ liệu mới
Tạo file JavaScript mới trong thư mục `data/` với cấu trúc như sau:

```javascript
const tenBien = {
    "data": [
        {
            "id": 1,
            "name": "Tên điểm",
            "code": "Mã điểm",
            "address": "Địa chỉ",
            "lat": "10.123456",
            "long": "106.123456",
            // Các trường khác tùy theo loại dữ liệu
        }
        // ... thêm các điểm khác
    ],
    "metadata": {
        "type": "loai_du_lieu",
        "description": "Mô tả loại dữ liệu",
        "color": "#MãMàu",
        "icon": "🏷️"
    }
};
```

### 2. Cập nhật file HTML
Thêm script tag vào file `optimized_map_ekmap_free.html`:

```html
<script src="data/ten_file_moi.js"></script>
```

### 3. Đăng ký nguồn dữ liệu
Thêm vào hàm `loadAllDataSources()` trong file HTML:

```javascript
registerDataSource('tenBien', tenBien, {
    type: 'loai_du_lieu',
    name: 'Tên hiển thị',
    icon: '🏷️',
    colors: {
        'loai_du_lieu': '#MãMàu'
    }
});
```

### 4. Xử lý dữ liệu (nếu cần)
Thêm logic xử lý trong hàm `processDataSource()` nếu cần xử lý đặc biệt cho loại dữ liệu mới.

## Ví dụ các loại dữ liệu

### Điểm bán hàng (data_users.js) - Rule đặc biệt
- **Màu đỏ**: Khách hàng đối tác (sync_dms = null)
- **Màu cam**: Khách hàng nội bộ (sync_dms = "Y")
- **Icon cố định**: 🏪
- **Rule**: Phải tuân theo rule sync_dms để phân loại màu sắc

### Kho nhà PP
- **Màu xanh lá**: Kho nhà PP
- **Icon ngẫu nhiên**: Tự động chọn từ danh sách icon
- **Hiển thị**: Sức chứa, trạng thái, quản lý

### Các file dữ liệu khác
- **Icon ngẫu nhiên**: Tự động chọn từ danh sách icon
- **Màu sắc**: Tùy chỉnh theo config
- **Hiển thị**: Thông tin cơ bản + thông tin đặc thù

## Lưu ý
- Tất cả tọa độ phải ở định dạng string
- ID phải là số duy nhất
- Tên file và tên biến phải khớp nhau
- Màu sắc nên sử dụng mã hex (#RRGGBB)
