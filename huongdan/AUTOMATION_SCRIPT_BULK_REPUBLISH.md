# AUTOMATION SCRIPTS: BULK RE-PUBLISH CONTENT ITEMS

## 🎯 MỤC ĐÍCH
Tự động re-publish hàng loạt Content Items để áp dụng Display Text Pattern mới, tiết kiệm thời gian thay vì làm thủ công.

## 🔧 SCRIPT POWERSHELL (CHO ADMIN)

### Script 1: Re-publish theo Content Type
```powershell
# Bulk re-publish Content Items by Content Type
param(
    [Parameter(Mandatory=$true)]
    [string]$ContentType,
    
    [Parameter(Mandatory=$false)]
    [string]$OrchardUrl = "https://localhost:5001",
    
    [Parameter(Mandatory=$false)]
    [string]$AdminPath = "/Admin"
)

Write-Host "Starting bulk re-publish for Content Type: $ContentType" -ForegroundColor Green

# Sử dụng OrchardCore Management APIs
$apiUrl = "$OrchardUrl$AdminPath/Api/Content"

try {
    # Get all content items of specified type
    $response = Invoke-RestMethod -Uri "$apiUrl?contentType=$ContentType" -Method GET
    
    $items = $response.contentItems
    $totalItems = $items.Count
    
    Write-Host "Found $totalItems items to re-publish" -ForegroundColor Yellow
    
    $counter = 0
    foreach ($item in $items) {
        $counter++
        Write-Progress -Activity "Re-publishing Content Items" -Status "Processing $($item.DisplayText)" -PercentComplete (($counter / $totalItems) * 100)
        
        # Re-publish item
        $publishUrl = "$apiUrl/$($item.ContentItemId)/publish"
        Invoke-RestMethod -Uri $publishUrl -Method POST
        
        Write-Host "[$counter/$totalItems] Re-published: $($item.DisplayText)" -ForegroundColor Cyan
        
        # Small delay to avoid overwhelming the server
        Start-Sleep -Milliseconds 500
    }
    
    Write-Host "✅ Successfully re-published $totalItems items!" -ForegroundColor Green
}
catch {
    Write-Host "❌ Error: $($_.Exception.Message)" -ForegroundColor Red
}
```

### Script 2: Re-publish tất cả Content Types
```powershell
# Re-publish all content items (use with caution!)
param(
    [Parameter(Mandatory=$false)]
    [string]$OrchardUrl = "https://localhost:5001",
    
    [Parameter(Mandatory=$false)]
    [string[]]$ContentTypes = @("FooterSocial", "FooterContact", "FooterAbout")
)

Write-Host "Starting bulk re-publish for multiple Content Types" -ForegroundColor Green

foreach ($contentType in $ContentTypes) {
    Write-Host "`n🔄 Processing Content Type: $contentType" -ForegroundColor Magenta
    
    # Call the first script for each content type
    & .\BulkRePublish.ps1 -ContentType $contentType -OrchardUrl $OrchardUrl
}

Write-Host "`n🎉 All Content Types processed!" -ForegroundColor Green
```

## 💻 C# CODE (CHO DEVELOPER)

### Service Class
```csharp
using OrchardCore.ContentManagement;
using OrchardCore.ContentManagement.Records;
using Microsoft.Extensions.Logging;
using YesSql;

public class BulkContentService
{
    private readonly IContentManager _contentManager;
    private readonly ISession _session;
    private readonly ILogger<BulkContentService> _logger;

    public BulkContentService(
        IContentManager contentManager,
        ISession session,
        ILogger<BulkContentService> logger)
    {
        _contentManager = contentManager;
        _session = session;
        _logger = logger;
    }

    public async Task<int> BulkRePublishByContentTypeAsync(string contentType)
    {
        _logger.LogInformation($"Starting bulk re-publish for Content Type: {contentType}");

        var contentItems = await _session
            .Query<ContentItem, ContentItemIndex>()
            .Where(x => x.ContentType == contentType && x.Published)
            .ListAsync();

        var count = 0;
        foreach (var item in contentItems)
        {
            try
            {
                await _contentManager.PublishAsync(item);
                count++;
                _logger.LogInformation($"Re-published: {item.DisplayText} (ID: {item.ContentItemId})");
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, $"Failed to re-publish item: {item.ContentItemId}");
            }
        }

        _logger.LogInformation($"✅ Successfully re-published {count} items of type {contentType}");
        return count;
    }

    public async Task<Dictionary<string, int>> BulkRePublishMultipleTypesAsync(string[] contentTypes)
    {
        var results = new Dictionary<string, int>();

        foreach (var contentType in contentTypes)
        {
            var count = await BulkRePublishByContentTypeAsync(contentType);
            results[contentType] = count;
        }

        return results;
    }
}
```

### Controller Action
```csharp
[HttpPost]
public async Task<IActionResult> BulkRePublish([FromBody] BulkRePublishRequest request)
{
    try
    {
        var bulkService = HttpContext.RequestServices.GetService<BulkContentService>();
        
        if (request.ContentTypes?.Any() == true)
        {
            var results = await bulkService.BulkRePublishMultipleTypesAsync(request.ContentTypes);
            return Json(new { success = true, results });
        }
        else if (!string.IsNullOrEmpty(request.ContentType))
        {
            var count = await bulkService.BulkRePublishByContentTypeAsync(request.ContentType);
            return Json(new { success = true, count });
        }

        return BadRequest("No content type specified");
    }
    catch (Exception ex)
    {
        return Json(new { success = false, error = ex.Message });
    }
}

public class BulkRePublishRequest
{
    public string ContentType { get; set; }
    public string[] ContentTypes { get; set; }
}
```

## 🌐 JAVASCRIPT (CHO ADMIN PANEL)

### Admin Panel Extension
```javascript
// Add to admin theme or create custom admin script
function bulkRePublishContentType(contentType) {
    if (!confirm(`Are you sure you want to re-publish all ${contentType} items?`)) {
        return;
    }

    const progressDiv = document.createElement('div');
    progressDiv.innerHTML = `
        <div class="alert alert-info">
            <strong>Processing...</strong> Re-publishing ${contentType} items
            <div class="progress mt-2">
                <div class="progress-bar" role="progressbar" style="width: 0%"></div>
            </div>
        </div>
    `;
    document.body.appendChild(progressDiv);

    fetch('/Admin/Api/BulkRePublish', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'RequestVerificationToken': document.querySelector('input[name="__RequestVerificationToken"]').value
        },
        body: JSON.stringify({ contentType: contentType })
    })
    .then(response => response.json())
    .then(data => {
        if (data.success) {
            progressDiv.innerHTML = `
                <div class="alert alert-success">
                    <strong>✅ Success!</strong> Re-published ${data.count} ${contentType} items
                </div>
            `;
            setTimeout(() => {
                location.reload();
            }, 2000);
        } else {
            progressDiv.innerHTML = `
                <div class="alert alert-danger">
                    <strong>❌ Error:</strong> ${data.error}
                </div>
            `;
        }
    })
    .catch(error => {
        progressDiv.innerHTML = `
            <div class="alert alert-danger">
                <strong>❌ Error:</strong> ${error.message}
            </div>
        `;
    });
}

// Add buttons to Content Types list
document.addEventListener('DOMContentLoaded', function() {
    const contentTypeRows = document.querySelectorAll('[data-content-type]');
    
    contentTypeRows.forEach(row => {
        const contentType = row.getAttribute('data-content-type');
        const actionsCell = row.querySelector('.actions');
        
        if (actionsCell) {
            const bulkButton = document.createElement('button');
            bulkButton.className = 'btn btn-sm btn-outline-secondary';
            bulkButton.innerHTML = '🔄 Bulk Re-publish';
            bulkButton.onclick = () => bulkRePublishContentType(contentType);
            
            actionsCell.appendChild(bulkButton);
        }
    });
});
```

## 📋 HƯỚNG DẪN SỬ DỤNG

### PowerShell Script:
1. Lưu script thành file `.ps1`
2. Mở PowerShell as Administrator
3. Chạy: `.\BulkRePublish.ps1 -ContentType "FooterSocial"`

### C# Service:
1. Thêm service vào DI container
2. Inject vào Controller hoặc Background Service
3. Gọi method `BulkRePublishByContentTypeAsync`

### JavaScript:
1. Thêm vào admin theme
2. Buttons sẽ xuất hiện tự động trong Content Types list
3. Click để bulk re-publish

## ⚠️ LƯU Ý AN TOÀN

1. **Backup database trước khi chạy**
2. **Test trên môi trường dev trước**
3. **Chạy trong giờ ít traffic**
4. **Monitor server resources**
5. **Có thể rollback nếu cần**

## 📊 PERFORMANCE

| Số lượng items | Thời gian thủ công | Thời gian script |
|----------------|-------------------|------------------|
| 10 items | 5-10 phút | 10-30 giây |
| 50 items | 25-50 phút | 1-2 phút |
| 100 items | 50-100 phút | 2-5 phút |
| 500 items | 4-8 giờ | 10-20 phút |

---

**Lưu ý:** Scripts này được thiết kế dựa trên OrchardCore 2.2.1. Có thể cần điều chỉnh cho các phiên bản khác.