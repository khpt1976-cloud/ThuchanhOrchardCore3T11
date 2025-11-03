# 📋 HƯỚNG DẪN CHI TIẾT BƯỚC 3: TẠO CONTENT TYPES CHO FOOTER

## 🎯 MỤC TIÊU
Tạo 3 Content Types cho Footer: **FooterContact**, **FooterSocial**, **FooterAbout**

---

## 🔄 FLOWCHART TỔNG QUAN

```
START
  ↓
[Đăng nhập Admin Panel]
  ↓
[Vào Content → Content Definition → Content Types]
  ↓
[Tạo Content Type 1: FooterContact]
  ↓
[Tạo Content Type 2: FooterSocial]  
  ↓
[Tạo Content Type 3: FooterAbout]
  ↓
[Kiểm tra kết quả]
  ↓
END
```

---

## 📝 CHI TIẾT TỪNG BƯỚC

### BƯỚC 3.1: TRUY CẬP CONTENT TYPES

#### 🖱️ Các thao tác click:
1. **Đăng nhập Admin Panel**: `http://localhost:5000/Admin`
2. **Click menu "Content"** (bên trái màn hình)
3. **Click "Content Definition"** (submenu mở ra)
4. **Click "Content Types"**

#### 📍 Vị trí hiện tại:
- URL: `/Admin/ContentTypes/List`
- Trang: Danh sách Content Types

---

### BƯỚC 3.2: TẠO CONTENT TYPE 1 - FOOTERCONTACT

#### 🔄 Flowchart chi tiết:

```
[Trang Content Types List]
  ↓
[Click "Create new type"]
  ↓
[Điền thông tin cơ bản]
  ↓
[Thiết lập Stereotype = "Widget"]
  ↓
[Click "Create"]
  ↓
[Thêm 4 Fields]
  ↓
[Click "Save"]
```

#### 📋 Thao tác chi tiết:

**Bước 3.2.1: Tạo Content Type**
1. **Click nút "Create new type"** (màu xanh, góc trên bên phải)
2. **Điền form tạo Content Type:**
   - **Technical Name**: `FooterContact`
   - **Display Name**: `Footer Contact`
   - **Description**: `Thông tin liên hệ cho Footer`
   - **Stereotype**: `Widget` ⚠️ **QUAN TRỌNG!**
3. **Click "Create"**

**Bước 3.2.2: Thêm Fields**

Sau khi tạo xong, tự động chuyển đến trang Edit Content Type.

**Field 1: Tên Công Ty**
1. **Click "Add Field"**
2. **Chọn "Text Field"** từ danh sách
3. **Điền thông tin:**
   - **Display Name**: `Tên Công Ty`
   - **Technical Name**: `CompanyName` (tự động)
4. **Click "Add"**

**Field 2: Địa Chỉ**
1. **Click "Add Field"**
2. **Chọn "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Địa Chỉ`
   - **Technical Name**: `Address`
4. **Click "Add"**

**Field 3: Số Điện Thoại**
1. **Click "Add Field"**
2. **Chọn "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Số Điện Thoại`
   - **Technical Name**: `PhoneNumber`
4. **Click "Add"**

**Field 4: Email**
1. **Click "Add Field"**
2. **Chọn "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Email`
   - **Technical Name**: `Email`
4. **Click "Add"**

**Bước 3.2.3: Lưu Content Type**
1. **Click "Save"** (nút màu xanh)
2. **Kiểm tra thông báo**: "The content type has been saved"

---

### BƯỚC 3.3: TẠO CONTENT TYPE 2 - FOOTERSOCIAL

#### 📋 Thao tác chi tiết:

**Bước 3.3.1: Tạo Content Type**
1. **Quay lại Content Types List**: Click "Content Types" trong breadcrumb
2. **Click "Create new type"**
3. **Điền form:**
   - **Technical Name**: `FooterSocial`
   - **Display Name**: `Footer Social`
   - **Description**: `Mạng xã hội cho Footer`
   - **Stereotype**: `Widget` ⚠️ **QUAN TRỌNG!**
4. **Click "Create"**

**Bước 3.3.2: Thêm Fields**

**Field 1: Tên Nền Tảng**
1. **Click "Add Field"**
2. **Chọn "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Tên Nền Tảng`
   - **Technical Name**: `PlatformName`
4. **Click "Add"**

**Field 2: Đường Dẫn Mạng Xã Hội**
1. **Click "Add Field"**
2. **Chọn "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Đường Dẫn Mạng Xã Hội`
   - **Technical Name**: `SocialLink`
4. **Click "Add"**

**Field 3: Lớp Icon**
1. **Click "Add Field"**
2. **Chọn "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Lớp Icon`
   - **Technical Name**: `IconClass`
4. **Click "Add"**

**Bước 3.3.3: Lưu Content Type**
1. **Click "Save"**

---

### BƯỚC 3.4: TẠO CONTENT TYPE 3 - FOOTERABOUT

#### 📋 Thao tác chi tiết:

**Bước 3.4.1: Tạo Content Type**
1. **Quay lại Content Types List**
2. **Click "Create new type"**
3. **Điền form:**
   - **Technical Name**: `FooterAbout`
   - **Display Name**: `Footer About`
   - **Description**: `Thông tin giới thiệu cho Footer`
   - **Stereotype**: `Widget` ⚠️ **QUAN TRỌNG!**
4. **Click "Create"**

**Bước 3.4.2: Thêm Fields**

**Field 1: Tiêu Đề Giới Thiệu**
1. **Click "Add Field"**
2. **Chọn "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Tiêu Đề Giới Thiệu`
   - **Technical Name**: `AboutTitle`
4. **Click "Add"**

**Field 2: Nội Dung Giới Thiệu**
1. **Click "Add Field"**
2. **Chọn "Html Field"** (để có thể định dạng text)
3. **Điền thông tin:**
   - **Display Name**: `Nội Dung Giới Thiệu`
   - **Technical Name**: `AboutContent`
4. **Click "Add"**

**Bước 3.4.3: Lưu Content Type**
1. **Click "Save"**

---

## ✅ KIỂM TRA KẾT QUẢ

### Bước 1: Kiểm tra Content Types List
1. **Vào Content → Content Definition → Content Types**
2. **Xác nhận có 3 Content Types mới:**
   - ✅ FooterContact
   - ✅ FooterSocial  
   - ✅ FooterAbout

### Bước 2: Kiểm tra Widget availability
1. **Vào Design → Widgets**
2. **Click "Add Widget"**
3. **Xác nhận 3 Content Types xuất hiện trong danh sách:**
   - ✅ Footer Contact
   - ✅ Footer Social
   - ✅ Footer About

---

## ⚠️ LƯU Ý QUAN TRỌNG

### 🔴 Điểm quan trọng nhất:
- **PHẢI thiết lập Stereotype = "Widget"** cho tất cả 3 Content Types
- Nếu không có Stereotype = "Widget", Content Types sẽ không xuất hiện trong Design → Widgets

### 🔧 Các Field Types được sử dụng:
- **Text Field**: Cho các thông tin văn bản ngắn
- **Html Field**: Cho nội dung có thể định dạng (chỉ dùng cho AboutContent)

### 📱 Technical Names:
- Phải viết liền, không dấu, PascalCase
- Ví dụ: `CompanyName`, `SocialLink`, `AboutTitle`

---

## 🎯 KẾT QUẢ MONG ĐỢI

Sau khi hoàn thành BƯỚC 3, bạn sẽ có:

1. **3 Content Types mới** với Stereotype = "Widget"
2. **Tổng cộng 9 Fields** được tạo:
   - FooterContact: 4 fields
   - FooterSocial: 3 fields  
   - FooterAbout: 2 fields
3. **Có thể tạo Widgets** từ 3 Content Types này trong Design → Widgets

---

## 🚀 BƯỚC TIẾP THEO

Sau khi hoàn thành BƯỚC 3, bạn có thể:
- **BƯỚC 4**: Tạo các Widget instances từ Content Types
- **BƯỚC 5**: Gán Widgets vào Footer Zone
- **BƯỚC 6**: Tùy chỉnh giao diện Footer

---

*📝 Hướng dẫn này được tạo để hỗ trợ việc thực hành OrchardCore một cách chi tiết và dễ hiểu.*