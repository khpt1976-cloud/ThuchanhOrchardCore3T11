# PHÂN TÍCH DISPLAY TEXT PATTERN TRONG ORCHARDCORE

## 🔍 TÓM TẮT VẤN ĐỀ

Sau khi nghiên cứu source code OrchardCore và thực hiện debug, chúng ta đã tìm ra nguyên nhân và giải pháp cho vấn đề Display Text Pattern.

## 📊 PHÂN TÍCH SOURCE CODE ORCHARDCORE

### 1. Cách OrchardCore gốc hoạt động

Từ file `src/OrchardCore.Themes/TheAgencyTheme/Recipes/agency.recipe.json`:

```json
{
  "ContentItemId": "[js:uuid()]",
  "ContentType": "Service",
  "DisplayText": "E-Commerce",  // ← Set trực tiếp
  "TitlePart": {
    "Title": "E-Commerce"        // ← Cùng giá trị với DisplayText
  }
}
```

**Kết luận:** OrchardCore gốc **KHÔNG sử dụng Display Text Pattern**, mà set trực tiếp cả `DisplayText` và `TitlePart.Title`.

### 2. Widget Templates trong OrchardCore

Từ `src/OrchardCore.Themes/TheAgencyTheme/Views/Widget-Blockquote.liquid`:

```liquid
<article class="{{ Model.Classes | join: " " }}">
    <blockquote>
        {{ Model.ContentItem.Content.Blockquote.Quote.Text }}
    </blockquote>
</article>
```

**Cú pháp đúng:** `{{ Model.ContentItem.Content.[ContentType].[FieldName].Text }}`

## ⚠️ VẤN ĐỀ CỦA CHÚNG TA

### 1. Cú pháp sai ban đầu
```liquid
❌ SAI: {{ ContentItem.FooterSocial.SocialName.Text }}
✅ ĐÚNG: {{ ContentItem.Content.FooterSocial.SocialName.Text }}
```

### 2. Display Text Pattern chỉ áp dụng cho Content Items mới

| Content Item | Trạng thái | DisplayText | Lý do |
|-------------|------------|-------------|-------|
| Pinterest Test | ✅ Hoạt động | "Pinterest Test" | Được Publish lại sau khi sửa Pattern |
| TEST NEW PATTERN | ✅ Hoạt động | "TEST NEW PATTERN" | Tạo mới sau khi sửa Pattern |
| Facebook, Twitter, Instagram... | ❌ Chưa hoạt động | "FooterSocial" | Chưa được Publish lại |
| FooterContact | ❌ Chưa hoạt động | "FooterContact" | Chưa được Publish lại |
| FooterAbout | ❌ Chưa hoạt động | "FooterAbout" | Chưa được Publish lại |

## 🔧 GIẢI PHÁP

### Phương án 1: Publish lại tất cả Content Items cũ (KHUYẾN NGHỊ)

1. **Đã sửa cú pháp đúng:**
   - FooterSocial: `{{ ContentItem.Content.FooterSocial.SocialName.Text }}`
   - FooterContact: `{{ ContentItem.Content.FooterContact.ContactInfo.Text }}`
   - FooterAbout: `{{ ContentItem.Content.FooterAbout.AboutTitle.Text }}`

2. **Cần Publish lại từng Content Item:**
   - Vào Edit từng item cũ
   - Click "Publish" để áp dụng Pattern mới

### Phương án 2: Không dùng Display Text Pattern (như OrchardCore gốc)

1. Xóa Display Text Pattern khỏi TitlePart Settings
2. Set trực tiếp DisplayText khi tạo Content Items
3. Ưu điểm: Đơn giản, ổn định
4. Nhược điểm: Phải set manual cho từng item

## 🧪 KIỂM CHỨNG

### Test case đã thành công:
1. ✅ Sửa FooterSocial Pattern thành `{{ ContentItem.Content.FooterSocial.SocialName.Text }}`
2. ✅ Tạo item mới "TEST NEW PATTERN" → Hoạt động đúng
3. ✅ Publish lại item "Pinterest Test" → Hoạt động đúng

### Còn cần làm:
1. ⏳ Publish lại các FooterSocial items cũ (Facebook, Twitter, Instagram...)
2. ⏳ Sửa và test FooterContact Pattern
3. ⏳ Sửa và test FooterAbout Pattern

## 📝 KẾT LUẬN

**Display Text Pattern HOẠT ĐỘNG ĐÚNG** với cú pháp:
```liquid
{{ ContentItem.Content.[ContentTypeName].[FieldName].Text }}
```

**Vấn đề chính:** Content Items cũ cần được Publish lại để áp dụng Pattern mới.

**Khuyến nghị:** Tiếp tục sử dụng Display Text Pattern vì nó linh hoạt và tự động hóa việc tạo title.

---

**Ngày tạo:** 2025-11-02  
**Trạng thái:** Display Text Pattern đã hoạt động cho items mới và items được publish lại  
**Cần làm tiếp:** Publish lại các Content Items cũ để hoàn thành