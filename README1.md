# Kochi Lens Website
## Software Requirement Specification (SRS)
### Chức năng 2.1 – Quản lý Sản phẩm (PIM)

---

# PHẦN 1: MÔ HÌNH HÓA QUY TRÌNH (BUSINESS FLOW)

---

## 1.1 Sơ đồ Use Case

### Actor trong hệ thống

| Actor | Mô tả |
|---|---|
| Admin | Quản lý sản phẩm và biến thể |
| Warehouse Staff | Quản lý tồn kho |
| Customer | Xem sản phẩm và đặt hàng |

---

### Use Case

#### Admin
- Tạo sản phẩm
- Cập nhật sản phẩm
- Quản lý biến thể (Màu sắc, kích thước)
- Cập nhật giá bán
- Upload hình ảnh
- Bật/Tắt sản phẩm

#### Warehouse Staff
- Nhập kho sản phẩm
- Điều chỉnh tồn kho
- Cập nhật số lượng tồn

#### Customer
- Xem danh sách sản phẩm
- Xem chi tiết sản phẩm
- Chọn biến thể
- Thêm sản phẩm vào giỏ hàng

---

## 1.2 Sơ đồ Activity  
### Luồng đặt hàng từ chọn sản phẩm → thanh toán thành công

1. Customer truy cập website
2. Hệ thống hiển thị danh sách sản phẩm từ PIM
3. Customer chọn sản phẩm
4. Hệ thống hiển thị biến thể sản phẩm
5. Customer chọn biến thể
6. Hệ thống kiểm tra tồn kho realtime
7. Customer thêm sản phẩm vào giỏ hàng
8. Customer tiến hành thanh toán
9. Thanh toán thành công
10. Hệ thống xác nhận đơn hàng
11. Hệ thống cập nhật tồn kho

---

# PHẦN 2: ĐẶC TẢ CHỨC NĂNG (FUNCTIONAL REQUIREMENTS)

---

## User Story

### Quản lý sản phẩm
- Là **Admin**, tôi muốn tạo sản phẩm mới để bán trên website.
- Là **Admin**, tôi muốn chỉnh sửa thông tin sản phẩm để cập nhật dữ liệu chính xác.
- Là **Admin**, tôi muốn upload hình ảnh sản phẩm để khách hàng dễ xem.

### Quản lý biến thể
- Là **Admin**, tôi muốn tạo biến thể màu sắc hoặc kích thước cho sản phẩm.
- Là **Customer**, tôi muốn chọn biến thể trước khi mua để đúng nhu cầu.

### Tồn kho realtime
- Là **Warehouse Staff**, tôi muốn cập nhật số lượng tồn kho để hệ thống phản ánh đúng thực tế.
- Là **Customer**, tôi muốn thấy số lượng còn hàng để quyết định mua.

### Giá bán
- Là **Admin**, tôi muốn thiết lập giá bán và thuế VAT cho sản phẩm.
- Là **Customer**, tôi muốn xem giá chính xác trước khi thanh toán.

---

# PHẦN 3: ĐẶC TẢ DỮ LIỆU (DATA SCHEMA)

---

## 3.1 Partner (Khách hàng)

| Trường | Kiểu dữ liệu | Mô tả |
|---|---|---|
| Partner_ID | UUID | Mã khách hàng |
| Name | String | Tên khách hàng |
| Company_Name | String | Tên công ty (nếu B2B) |
| Tax_Code | String | Mã số thuế |
| Shipping_Address | Text | Địa chỉ giao hàng |
| Email | String | Email liên hệ |
| Phone | String | Số điện thoại |

---

## 3.2 Product (Sản phẩm)

| Trường | Kiểu dữ liệu | Mô tả |
|---|---|---|
| Product_ID | UUID | ID sản phẩm |
| Product_Name | String | Tên sản phẩm |
| SKU | String | Mã SKU |
| Barcode | String | Mã vạch |
| Sale_Price | Decimal | Giá bán |
| VAT | Decimal | Thuế VAT (%) |
| Description | Text | Mô tả sản phẩm |
| Status | Boolean | Trạng thái sản phẩm |

---

## 3.3 Order (Đơn hàng)

| Trường | Kiểu dữ liệu | Mô tả |
|---|---|---|
| Order_ID | UUID | ID đơn hàng |
| Order_Number | String | Số đơn hàng |
| Partner_ID | FK | Khách hàng |
| Order_Status | Enum | Draft / Confirmed / Cancelled |
| Total_Amount | Decimal | Tổng tiền đơn hàng |
| Created_Date | Datetime | Ngày tạo |

---

# KẾT LUẬN

Chức năng **Quản lý Sản phẩm (PIM)** giúp:

- Quản lý thông tin sản phẩm
- Quản lý biến thể
- Hiển thị tồn kho realtime
- Hỗ trợ quy trình đặt hàng trực tuyến