# 📋 BƯỚC 3: TẠO CONTENT TYPES CHO FOOTER

## 🎯 Mục tiêu
Tạo các Content Types để lưu trữ thông tin Footer có thể quản trị qua Admin Panel.

## 📚 Kiến thức cần biết
- **Content Type**: Định nghĩa cấu trúc dữ liệu
- **Content Field**: Các trường dữ liệu (Text, HTML, Link...)
- **Stereotype**: Phân loại Content Type (Widget, Content...)

## 📝 Các Content Types cần tạo

### 1. FooterContact (Thông tin liên hệ)
### 2. FooterSocial (Mạng xã hội)
### 3. FooterAbout (Giới thiệu)

---

## 🔄 FLOWCHART TỔNG QUAN

```
START: Đăng nhập Admin Panel
  ↓
[Vào Content → Content Definition → Content Types]
  ↓
[Tạo FooterContact Content Type + 4 Fields]
  ↓
[Tạo FooterSocial Content Type + 3 Fields]
  ↓
[Tạo FooterAbout Content Type + 2 Fields]
  ↓
[Kiểm tra trong Design → Widgets]
  ↓
END: Hoàn thành 3 Content Types
```

---

## 🖱️ HƯỚNG DẪN CHI TIẾT TỪNG CLICK CHUỘT

### 🏢 BƯỚC 3.1: TẠO FOOTERCONTACT CONTENT TYPE

#### 📍 Bước 3.1.1: Truy cập Content Types
1. **Mở trình duyệt** và truy cập: `http://localhost:5000/Admin`
2. **Đăng nhập** với tài khoản Admin
3. **Click vào menu "Content"** (bên trái màn hình, có icon 📄)
4. **Click vào "Content Definition"** (submenu sẽ mở ra)
5. **Click vào "Content Types"** 
   - 📍 **Vị trí hiện tại**: `/Admin/ContentTypes/List`
   - 👀 **Bạn sẽ thấy**: Danh sách các Content Types hiện có

#### 📝 Bước 3.1.2: Tạo Content Type mới
1. **Click nút "Create new type"** 
   - 🎨 **Màu**: Xanh lá
   - 📍 **Vị trí**: Góc trên bên phải
2. **Điền form tạo Content Type:**

   **🔤 Technical Name:**
   - Click vào ô "Technical Name"
   - Gõ: `FooterContact`
   - ⚠️ **Lưu ý**: Viết liền, không dấu, không khoảng trắng

   **📝 Display Name:**
   - Click vào ô "Display Name"  
   - Gõ: `Footer Contact`

   **📄 Description:**
   - Click vào ô "Description"
   - Gõ: `Thông tin liên hệ trong Footer`

   **🏷️ Stereotype:** ⚠️ **QUAN TRỌNG NHẤT!**
   - Click vào dropdown "Stereotype"
   - Gõ: `Widget`
   - **Tại sao quan trọng?** Nếu không có Stereotype = "Widget", Content Type sẽ không xuất hiện trong Design → Widgets

3. **Click nút "Create"** (màu xanh)
   - 📍 **Chuyển đến**: Trang Edit Content Type
   - 👀 **Bạn sẽ thấy**: Form chỉnh sửa Content Type với các section Fields, Parts

#### 🔧 Bước 3.1.3: Thêm Fields cho FooterContact

**🏢 Field 1: Tên Công Ty**
1. **Click nút "Add Field"** (màu xanh)
2. **Chọn Field Type:**
   - 👀 **Bạn sẽ thấy**: Danh sách các loại Field
   - **Click "Text Field"**
3. **Điền thông tin Field:**
   - **Display Name**: Gõ `Tên Công Ty`
   - **Technical Name**: Tự động thành `CompanyName` (không cần sửa)
4. **Click "Add"** (màu xanh)
   - ✅ **Kết quả**: Field "Tên Công Ty" xuất hiện trong danh sách Fields

**🏠 Field 2: Địa Chỉ**
1. **Click nút "Add Field"** 
2. **Click "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Địa Chỉ`
   - **Technical Name**: `Address` (tự động)
4. **Click "Add"**

**📞 Field 3: Số Điện Thoại**
1. **Click nút "Add Field"**
2. **Click "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Số Điện Thoại`
   - **Technical Name**: `PhoneNumber` (tự động)
4. **Click "Add"**

**📧 Field 4: Email**
1. **Click nút "Add Field"**
2. **Click "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Email`
   - **Technical Name**: `Email` (tự động)
4. **Click "Add"**

#### 💾 Bước 3.1.4: Lưu Content Type
1. **Click nút "Save"** (màu xanh, ở cuối trang)
2. **Kiểm tra thông báo thành công:**
   - 👀 **Bạn sẽ thấy**: Thông báo màu xanh "The content type has been saved"
3. **Xác nhận kết quả:**
   - ✅ FooterContact Content Type đã được tạo
   - ✅ Có 4 Fields: Tên Công Ty, Địa Chỉ, Số Điện Thoại, Email
   - ✅ Stereotype = Widget

---

### 📱 BƯỚC 3.2: TẠO FOOTERSOCIAL CONTENT TYPE

#### 📍 Bước 3.2.1: Quay lại Content Types List
1. **Click "Content Types"** trong breadcrumb (đường dẫn ở trên)
   - 📍 **Quay về**: `/Admin/ContentTypes/List`
   - 👀 **Bạn sẽ thấy**: FooterContact đã xuất hiện trong danh sách

#### 📝 Bước 3.2.2: Tạo Content Type mới
1. **Click nút "Create new type"** (màu xanh)
2. **Điền form:**

   **🔤 Technical Name:**
   - Click vào ô "Technical Name"
   - Gõ: `FooterSocial`

   **📝 Display Name:**
   - Click vào ô "Display Name"
   - Gõ: `Footer Social`

   **📄 Description:**
   - Click vào ô "Description"
   - Gõ: `Liên kết mạng xã hội trong Footer`

   **🏷️ Stereotype:** ⚠️ **QUAN TRỌNG!**
   - Click vào dropdown "Stereotype"
   - Gõ: `Widget`

3. **Click nút "Create"** (màu xanh)

#### 🔧 Bước 3.2.3: Thêm Fields cho FooterSocial

**📱 Field 1: Tên Nền Tảng**
1. **Click nút "Add Field"**
2. **Click "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Tên Nền Tảng`
   - **Technical Name**: `PlatformName` (tự động)
4. **Click "Add"**

**🔗 Field 2: Đường Dẫn Mạng Xã Hội**
1. **Click nút "Add Field"**
2. **Click "Text Field"** (dùng Text Field thay vì Link Field cho đơn giản)
3. **Điền thông tin:**
   - **Display Name**: `Đường Dẫn Mạng Xã Hội`
   - **Technical Name**: `SocialLink` (tự động)
4. **Click "Add"**

**🎨 Field 3: Lớp Icon**
1. **Click nút "Add Field"**
2. **Click "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Lớp Icon`
   - **Technical Name**: `IconClass` (tự động)
4. **Click "Add"**

#### 💾 Bước 3.2.4: Lưu Content Type
1. **Click nút "Save"** (màu xanh)
2. **Xác nhận kết quả:**
   - ✅ FooterSocial Content Type đã được tạo
   - ✅ Có 3 Fields: Tên Nền Tảng, Đường Dẫn Mạng Xã Hội, Lớp Icon
   - ✅ Stereotype = Widget

---

### 📖 BƯỚC 3.3: TẠO FOOTERABOUT CONTENT TYPE

#### 📍 Bước 3.3.1: Quay lại Content Types List
1. **Click "Content Types"** trong breadcrumb
   - 📍 **Quay về**: `/Admin/ContentTypes/List`
   - 👀 **Bạn sẽ thấy**: FooterContact và FooterSocial đã có trong danh sách

#### 📝 Bước 3.3.2: Tạo Content Type mới
1. **Click nút "Create new type"** (màu xanh)
2. **Điền form:**

   **🔤 Technical Name:**
   - Click vào ô "Technical Name"
   - Gõ: `FooterAbout`

   **📝 Display Name:**
   - Click vào ô "Display Name"
   - Gõ: `Footer About`

   **📄 Description:**
   - Click vào ô "Description"
   - Gõ: `Thông tin giới thiệu trong Footer`

   **🏷️ Stereotype:** ⚠️ **QUAN TRỌNG!**
   - Click vào dropdown "Stereotype"
   - Gõ: `Widget`

3. **Click nút "Create"** (màu xanh)

#### 🔧 Bước 3.3.3: Thêm Fields cho FooterAbout

**📝 Field 1: Tiêu Đề Giới Thiệu**
1. **Click nút "Add Field"**
2. **Click "Text Field"**
3. **Điền thông tin:**
   - **Display Name**: `Tiêu Đề Giới Thiệu`
   - **Technical Name**: `AboutTitle` (tự động)
4. **Click "Add"**

**📄 Field 2: Nội Dung Giới Thiệu**
1. **Click nút "Add Field"**
2. **Tìm và Click "Html Field"** (để có thể định dạng text)
   - 👀 **Lưu ý**: Html Field cho phép định dạng văn bản (bold, italic, link...)
3. **Điền thông tin:**
   - **Display Name**: `Nội Dung Giới Thiệu`
   - **Technical Name**: `AboutContent` (tự động)
4. **Click "Add"**

#### 💾 Bước 3.3.4: Lưu Content Type
1. **Click nút "Save"** (màu xanh)
2. **Xác nhận kết quả:**
   - ✅ FooterAbout Content Type đã được tạo
   - ✅ Có 2 Fields: Tiêu Đề Giới Thiệu, Nội Dung Giới Thiệu
   - ✅ Stereotype = Widget

---

## ✅ KIỂM TRA KẾT QUẢ

### 🔍 Bước 4.1: Xác nhận Content Types đã tạo
1. **Vào Content → Content Types**
2. **Kiểm tra danh sách:**
   - ✅ **FooterContact** (Stereotype: Widget) - 4 Fields
   - ✅ **FooterSocial** (Stereotype: Widget) - 3 Fields
   - ✅ **FooterAbout** (Stereotype: Widget) - 2 Fields

### 🎨 Bước 4.2: Kiểm tra trong Widgets
1. **Click menu "Design"** (bên trái)
2. **Click "Widgets"**
3. **Click nút "Add Widget"** (màu xanh)
4. **Kiểm tra danh sách Widget Types:**
   - ✅ **Footer Contact** (xuất hiện trong danh sách)
   - ✅ **Footer Social** (xuất hiện trong danh sách)
   - ✅ **Footer About** (xuất hiện trong danh sách)

---

## 🎯 KẾT QUẢ MONG ĐỢI

### ✅ Đã hoàn thành:
- **3 Content Types** được tạo thành công
- **Tổng cộng 9 Fields** được tạo:
  - FooterContact: 4 fields (Tên Công Ty, Địa Chỉ, Số Điện Thoại, Email)
  - FooterSocial: 3 fields (Tên Nền Tảng, Đường Dẫn Mạng Xã Hội, Lớp Icon)
  - FooterAbout: 2 fields (Tiêu Đề Giới Thiệu, Nội Dung Giới Thiệu)
- **Tất cả đều có Stereotype = Widget**
- **Xuất hiện trong Design → Widgets → Add Widget**

---

## 🚀 BƯỚC TIẾP THEO

→ **BƯỚC 4**: Tạo Widget Templates để hiển thị Content Types
→ **BƯỚC 5**: Tạo Content Items từ các Content Types
→ **BƯỚC 6**: Setup Layers và Widgets cho Footer Zone

---

## ⚠️ GHI CHÚ QUAN TRỌNG

### 🔴 Điểm quan trọng nhất:
- **Stereotype: Widget** là BẮT BUỘC để Content Type xuất hiện trong Design → Widgets
- Nếu quên thiết lập Stereotype, Content Type sẽ chỉ xuất hiện trong Content Items, không thể dùng làm Widget

### 🔧 Các Field Types đã sử dụng:
- **Text Field**: Cho các thông tin văn bản ngắn (tên, địa chỉ, phone, email, platform, link, icon class, title)
- **Html Field**: Cho nội dung có thể định dạng (AboutContent)

### 📱 Technical Names:
- Phải viết liền, không dấu, PascalCase
- Ví dụ: `CompanyName`, `SocialLink`, `AboutTitle`, `AboutContent`

### 🎨 Display Names:
- Có thể có dấu, khoảng trắng, tiếng Việt
- Ví dụ: `Tên Công Ty`, `Đường Dẫn Mạng Xã Hội`, `Tiêu Đề Giới Thiệu`

---

## 🔄 FLOWCHART TỔNG KẾT

```
✅ HOÀN THÀNH BƯỚC 3
  ↓
[3 Content Types với Stereotype = Widget]
  ↓
[9 Fields tổng cộng đã được tạo]
  ↓
[Có thể tạo Widgets từ các Content Types]
  ↓
SẴN SÀNG CHO BƯỚC 4: TẠO WIDGET TEMPLATES
```

---

*📝 Hướng dẫn này được tạo để hỗ trợ việc thực hành OrchardCore một cách chi tiết và dễ hiểu. Mỗi bước đều có hướng dẫn click chuột cụ thể để người học có thể thực hiện chính xác.*