# HƯỚNG DẪN DISPLAY TEXT PATTERN TRONG ORCHARDCORE

## ⚠️ VẤN ĐỀ QUAN TRỌNG CẦN LƯU Ý

**Display Text Pattern chỉ áp dụng cho Content Items MỚI hoặc khi RE-PUBLISH Content Items cũ!**

## 🎯 CÚ PHÁP ĐÚNG

```liquid
{{ ContentItem.Content.[ContentTypeName].[FieldName].Text }}
```

### Ví dụ cụ thể:
- **FooterSocial**: `{{ ContentItem.Content.FooterSocial.SocialName.Text }}`
- **FooterContact**: `{{ ContentItem.Content.FooterContact.CompanyName.Text }}`
- **FooterAbout**: `{{ ContentItem.Content.FooterAbout.Title.Text }}`

## 🚨 LỖI THƯỜNG GẶP

### ❌ CÚ PHÁP SAI:
```liquid
{{ ContentItem.FooterSocial.SocialName.Text }}
```

### ✅ CÚ PHÁP ĐÚNG:
```liquid
{{ ContentItem.Content.FooterSocial.SocialName.Text }}
```

**Chú ý:** Phải có `.Content.` giữa `ContentItem` và `ContentTypeName`

## 📋 QUY TRÌNH THIẾT LẬP DISPLAY TEXT PATTERN

### Bước 1: Cấu hình Pattern
1. Vào **Admin → Content → Content Definition → Content Types**
2. Click **Edit** Content Type cần cấu hình
3. Tìm phần **Title Part**
4. Trong **Display Text Pattern**, nhập:
   ```liquid
   {{ ContentItem.Content.[ContentTypeName].[FieldName].Text }}
   ```
5. Click **Save**

### Bước 2: Xử lý Content Items
#### Với Content Items MỚI:
- Tạo bình thường → Pattern sẽ tự động áp dụng

#### Với Content Items CŨ (ĐÃ TỒN TẠI):
- **PHẢI RE-PUBLISH** để áp dụng Pattern mới
- Vào **Admin → Content → Content Items**
- Click **Edit** từng item cũ
- Click **Publish** (không cần thay đổi gì)
- Pattern sẽ được áp dụng

## ⏰ TẠI SAO MẤT THỜI GIAN?

### Nguyên nhân:
- OrchardCore chỉ thực thi Pattern khi ContentItem được **UPDATE/PUBLISH**
- Content Items cũ không tự động áp dụng Pattern mới
- Phải re-publish từng item một cách thủ công

### Từ tài liệu chính thức:
> *"The Pattern has access to the current ContentItem and is executed on ContentItem update."*

## 🛠️ GIẢI PHÁP TIẾT KIỆM THỜI GIAN

### 1. Thiết lập Pattern TRƯỚC khi tạo Content
- Cấu hình Display Text Pattern trước
- Tạo Content Items sau → Tự động áp dụng

### 2. Bulk Update (Nâng cao)
- Tạo script PowerShell/C# để bulk update
- Sử dụng OrchardCore APIs
- Áp dụng cho dự án lớn với nhiều Content Items

### 3. Workflow tự động
- Tạo Workflow tự động re-publish khi thay đổi Pattern
- Sử dụng OrchardCore Workflows module

## 📝 CHECKLIST KHI TẠO CONTENT TYPE MỚI

- [ ] Tạo Content Type với các Fields cần thiết
- [ ] **NGAY LẬP TỨC** cấu hình Display Text Pattern
- [ ] Test với 1 Content Item mẫu
- [ ] Xác minh Pattern hoạt động đúng
- [ ] Bắt đầu tạo Content Items thực tế

## 🔍 CÁCH KIỂM TRA PATTERN HOẠT ĐỘNG

### Dấu hiệu Pattern hoạt động:
- Content Item hiển thị tên cụ thể thay vì tên Content Type
- Ví dụ: "Facebook" thay vì "FooterSocial"

### Dấu hiệu Pattern CHƯA hoạt động:
- Content Item hiển thị tên Content Type generic
- Ví dụ: "FooterSocial" thay vì "Facebook"

## 🎯 BEST PRACTICES

### 1. Luôn thiết lập Pattern trước
```
Tạo Content Type → Cấu hình Pattern → Tạo Content Items
```

### 2. Test ngay lập tức
- Tạo 1 Content Item test
- Kiểm tra DisplayText
- Sửa Pattern nếu cần

### 3. Ghi chú Pattern đã sử dụng
```liquid
# FooterSocial
{{ ContentItem.Content.FooterSocial.SocialName.Text }}

# FooterContact  
{{ ContentItem.Content.FooterContact.CompanyName.Text }}

# FooterAbout
{{ ContentItem.Content.FooterAbout.Title.Text }}
```

### 4. Backup trước khi thay đổi Pattern
- Export Content Items
- Backup database
- Test trên môi trường dev trước

## 🚀 TƯƠNG LAI: AUTOMATION

### Script PowerShell mẫu (cho admin):
```powershell
# Bulk re-publish Content Items
$contentItems = Get-OrchardContentItems -ContentType "FooterSocial"
foreach ($item in $contentItems) {
    Publish-OrchardContentItem -Id $item.Id
    Write-Host "Re-published: $($item.DisplayText)"
}
```

### C# Code mẫu (cho developer):
```csharp
// Bulk update via OrchardCore APIs
var contentItems = await _contentManager.GetAsync(contentType: "FooterSocial");
foreach (var item in contentItems) {
    await _contentManager.PublishAsync(item);
}
```

## 📊 THỐNG KÊ THỜI GIAN

| Số lượng Content Items | Thời gian re-publish thủ công | Thời gian với script |
|------------------------|-------------------------------|---------------------|
| 10 items | ~5-10 phút | ~30 giây |
| 50 items | ~25-50 phút | ~2 phút |
| 100 items | ~50-100 phút | ~5 phút |

## 🎓 BÀI HỌC RÚT RA

1. **Luôn cấu hình Pattern TRƯỚC khi tạo Content**
2. **Hiểu rõ lifecycle của OrchardCore Content Items**
3. **Chuẩn bị script automation cho dự án lớn**
4. **Test Pattern ngay sau khi cấu hình**
5. **Ghi chú Pattern để tái sử dụng**

---

**Tác giả:** OpenHands AI Assistant  
**Ngày tạo:** 2025-11-02  
**Phiên bản OrchardCore:** 2.2.1  
**Trạng thái:** ✅ Đã kiểm chứng thực tế

**Lưu ý:** Tài liệu này được tạo dựa trên kinh nghiệm thực tế gặp phải vấn đề Display Text Pattern không hoạt động với existing Content Items.