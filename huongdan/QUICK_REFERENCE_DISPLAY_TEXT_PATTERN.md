# QUICK REFERENCE: DISPLAY TEXT PATTERN

## 🚨 NHỚ NGAY: Pattern chỉ áp dụng cho Content Items MỚI hoặc khi RE-PUBLISH!

## ✅ CÚ PHÁP ĐÚNG
```liquid
{{ ContentItem.Content.[ContentTypeName].[FieldName].Text }}
```

## 📋 QUY TRÌNH NHANH

### 1. Tạo Content Type mới
```
Admin → Content → Content Definition → Content Types → Create
```

### 2. NGAY LẬP TỨC cấu hình Pattern
```
Edit Content Type → Title Part → Display Text Pattern
```

### 3. Test với 1 Content Item
```
Tạo 1 item test → Kiểm tra DisplayText → OK thì tiếp tục
```

### 4. Nếu có Content Items cũ
```
Admin → Content → Content Items → Edit từng item → Publish
```

## 🔧 PATTERN TEMPLATES

### FooterSocial
```liquid
{{ ContentItem.Content.FooterSocial.SocialName.Text }}
```

### FooterContact
```liquid
{{ ContentItem.Content.FooterContact.CompanyName.Text }}
```

### FooterAbout
```liquid
{{ ContentItem.Content.FooterAbout.Title.Text }}
```

### Blog Post
```liquid
{{ ContentItem.Content.BlogPost.Title.Text }}
```

### Product
```liquid
{{ ContentItem.Content.Product.ProductName.Text }}
```

## ⚠️ TROUBLESHOOTING

### Vấn đề: Content Item hiển thị tên Content Type thay vì tên cụ thể
**Nguyên nhân:** Content Item được tạo TRƯỚC khi cấu hình Pattern
**Giải pháp:** Re-publish Content Item đó

### Vấn đề: Pattern không hoạt động
**Kiểm tra:**
1. Cú pháp có đúng không? (nhớ `.Content.`)
2. Tên Field có chính xác không?
3. Content Item đã được publish sau khi cấu hình Pattern chưa?

## 💡 TIPS TIẾT KIỆM THỜI GIAN

1. **Luôn cấu hình Pattern TRƯỚC khi tạo Content**
2. **Test ngay với 1 item mẫu**
3. **Ghi chú Pattern đã dùng để tái sử dụng**
4. **Với dự án lớn: viết script bulk update**

---
**Nhớ:** Cấu hình Pattern → Test → Tạo Content → Không phải re-publish!