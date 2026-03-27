## Kochi Lens Website
## Software Requirement Specification (SRS)
### Chức năng 2.1 — Quản lý Sản phẩm (PIM)

---

# 1. Giới thiệu

## 1.1 Mục đích
Tài liệu này mô tả yêu cầu phần mềm cho chức năng **Quản lý Sản phẩm (Product Information Management - PIM)** của hệ thống Kochi Lens.

Module PIM chịu trách nhiệm:
- Quản lý thông tin sản phẩm
- Quản lý biến thể sản phẩm
- Hiển thị tồn kho realtime
- Cung cấp dữ liệu cho hệ thống bán hàng

---

## 1.2 Phạm vi
Chức năng PIM cho phép:
- Admin quản lý sản phẩm
- Nhân viên kho quản lý tồn kho
- Khách hàng xem thông tin sản phẩm và số lượng còn hàng

---

# 2. Mô hình hóa quy trình (Business Flow)

---

## 2.1 Actor

| Actor | Vai trò |
|---|---|
| Admin | Quản lý sản phẩm |
| Warehouse Staff | Quản lý tồn kho |
| Customer | Xem sản phẩm |

---

## 2.2 Use Case

### Admin
- Thêm sản phẩm
- Chỉnh sửa sản phẩm
- Xóa sản phẩm
- Quản lý biến thể (màu sắc, kích thước)
- Cập nhật giá bán
- Upload hình ảnh sản phẩm
- Bật/Tắt trạng thái hiển thị

### Warehouse Staff
- Cập nhật tồn kho
- Điều chỉnh số lượng hàng

### Customer
- Xem danh sách sản phẩm
- Xem biến thể
- Kiểm tra tồn kho realtime

---

## 2.3 Activity Diagram — Luồng sử dụng sản phẩm

1. Admin tạo sản phẩm mới
2. Admin tạo biến thể sản phẩm
3. Nhân viên kho nhập số lượng tồn
4. Hệ thống lưu dữ liệu PIM
5. Khách hàng truy cập website
6. Hệ thống hiển thị sản phẩm
7. Hiển thị tồn kho realtime
8. Khách chọn biến thể sản phẩm

---

# 3. Đặc tả chức năng (Functional Requirements)

---

## 3.1 Quản lý sản phẩm

- Là **Admin**, tôi muốn tạo sản phẩm mới để bán trên website.
- Là **Admin**, tôi muốn chỉnh sửa thông tin sản phẩm.
- Là **Admin**, tôi muốn thêm mô tả và hình ảnh sản phẩm.
- Là **Admin**, tôi muốn bật/tắt trạng thái sản phẩm.

---

## 3.2 Quản lý biến thể sản phẩm

- Là **Admin**, tôi muốn tạo biến thể theo màu sắc.
- Là **Admin**, tôi muốn tạo biến thể theo kích thước.
- Mỗi biến thể phải có **SKU riêng**.
- Khách hàng phải chọn biến thể trước khi mua.

---

## 3.3 Quản lý tồn kho realtime

- Là **Warehouse Staff**, tôi muốn cập nhật số lượng tồn kho.
- Là **Hệ thống**, tôi muốn hiển thị tồn kho realtime.
- Là **Hệ thống**, tôi muốn ngăn chọn sản phẩm khi hết hàng.

---

## 3.4 Quản lý giá bán

- Là **Admin**, tôi muốn thiết lập giá bán cho sản phẩm.
- Là **Admin**, tôi muốn áp dụng thuế VAT.
- Là **Khách hàng**, tôi muốn thấy giá chính xác.

---

# 4. Đặc tả dữ liệu (Data Schema)

---

## 4.1 Product (Sản phẩm)

| Trường | Kiểu dữ liệu | Bắt buộc | Mô tả |
|---|---|---|---|
| Product_ID | UUID | ✔ | ID sản phẩm |
| Product_Name | String | ✔ | Tên sản phẩm |
| SKU | String | ✔ | Mã sản phẩm |
| Barcode | String | | Mã vạch |
| Category | String | ✔ | Danh mục |
| Brand | String | ✔ | Thương hiệu |
| Description | Text | | Mô tả |
| Sale_Price | Decimal | ✔ | Giá bán |
| VAT | Decimal | ✔ | Thuế VAT |
| Status | Boolean | ✔ | Active/Inactive |
| Created_Date | Datetime | ✔ | Ngày tạo |

---

## 4.2 Product Variant (Biến thể)

| Trường | Kiểu dữ liệu | Bắt buộc | Mô tả |
|---|---|---|---|
| Variant_ID | UUID | ✔ | ID biến thể |
| Product_ID | FK | ✔ | Liên kết sản phẩm |
| Color | String | ✔ | Màu sắc |
| Size | String | | Kích thước |
| Variant_SKU | String | ✔ | SKU biến thể |
| Sale_Price | Decimal | ✔ | Giá riêng |
| Stock_Qty | Integer | ✔ | Số lượng tồn |
| Available_Qty | Integer | ✔ | Có thể bán |
| Image_URL | URL | | Hình ảnh |

---

## 4.3 Inventory (Tồn kho)

| Trường | Kiểu | Mô tả |
|---|---|---|
| Inventory_ID | UUID | ID tồn kho |
| Variant_ID | FK | Biến thể |
| Quantity | Integer | Số lượng |
| Updated_By | User | Người cập nhật |
| Updated_Date | Datetime | Thời gian |

---

# 5. Tổng kết

Chức năng **PIM** đảm nhiệm:

- Quản lý dữ liệu sản phẩm
- Quản lý biến thể
- Quản lý tồn kho realtime
- Cung cấp dữ liệu sản phẩm cho hệ thống bán hàng