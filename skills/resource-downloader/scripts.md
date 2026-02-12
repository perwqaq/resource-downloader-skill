# 下载脚本模板

本文档提供资源下载的脚本模板和常用命令。

## PowerShell 下载命令

### 基本下载
```powershell
# 单文件下载
Invoke-WebRequest -Uri "https://example.com/image.jpg" -OutFile "image.jpg"

# 使用别名
wget "https://example.com/image.jpg" -OutFile "image.jpg"
```

### 批量下载
```powershell
# 从URL列表下载
$urls = @(
    "https://images.unsplash.com/photo-1",
    "https://images.unsplash.com/photo-2",
    "https://images.unsplash.com/photo-3"
)

$i = 1
foreach ($url in $urls) {
    $filename = "img-bg-tech-{0:D2}.jpg" -f $i
    Invoke-WebRequest -Uri $url -OutFile "assets/images/$filename"
    Write-Host "Downloaded: $filename"
    $i++
}
```

### 带进度显示
```powershell
function Download-File {
    param($Url, $Output)
    
    $client = New-Object System.Net.WebClient
    $client.DownloadFile($Url, $Output)
    Write-Host "Downloaded: $Output"
}

Download-File -Url "https://example.com/file.jpg" -Output "output.jpg"
```

## 常用资源网站直接下载链接

### Unsplash
```
# 图片ID格式
https://images.unsplash.com/photo-{ID}?w=1920&q=80

# 示例
https://images.unsplash.com/photo-1518770660439-4636190af475?w=1920&q=80
```

### Pexels
```
# 通过API获取下载链接
# 或直接访问图片页面获取
```

### Pixabay
```
# 图片ID格式
https://pixabay.com/get/{ID}
```

## 下载脚本示例

### 下载Unsplash图片
```powershell
function Get-UnsplashImage {
    param(
        [string]$PhotoId,
        [int]$Width = 1920,
        [int]$Quality = 80,
        [string]$OutputPath
    )
    
    $url = "https://images.unsplash.com/photo-$PhotoId?w=$Width&q=$Quality"
    Invoke-WebRequest -Uri $url -OutFile $OutputPath
    Write-Host "Downloaded to: $OutputPath"
}

# 使用示例
Get-UnsplashImage -PhotoId "1518770660439-4636190af475" -OutputPath "assets/images/img-bg-tech-01.jpg"
```

### 下载并转换格式
```powershell
# 需要安装 ImageMagick
function Download-And-Convert {
    param($Url, $OutputPath, $Format = "webp")
    
    $tempPath = "$env:TEMP\temp_image"
    Invoke-WebRequest -Uri $Url -OutFile $tempPath
    
    $finalPath = $OutputPath -replace '\.[^.]+$', ".$Format"
    magick convert $tempPath $finalPath
    
    Remove-Item $tempPath
    Write-Host "Converted and saved to: $finalPath"
}
```

## 资源清单生成

### 创建清单文件
```powershell
function New-ResourceManifest {
    param($Directory = "assets")
    
    $manifest = @{
        generatedAt = (Get-Date -Format "o")
        resources = @()
    }
    
    Get-ChildItem -Path $Directory -Recurse -File | ForEach-Object {
        $manifest.resources += @{
            path = $_.FullName
            name = $_.Name
            size = $_.Length
            type = $_.Extension.TrimStart('.')
        }
    }
    
    $manifest | ConvertTo-Json -Depth 10 | Out-File "resources-manifest.json"
    Write-Host "Manifest created with $($manifest.resources.Count) resources"
}
```

## 错误处理

### 带重试的下载
```powershell
function Download-With-Retry {
    param(
        [string]$Url,
        [string]$Output,
        [int]$MaxRetries = 3
    )
    
    $attempt = 1
    while ($attempt -le $MaxRetries) {
        try {
            Invoke-WebRequest -Uri $Url -OutFile $Output -TimeoutSec 30
            Write-Host "Success: $Output"
            return $true
        }
        catch {
            Write-Host "Attempt $attempt failed: $($_.Exception.Message)"
            $attempt++
            Start-Sleep -Seconds 2
        }
    }
    
    Write-Host "Failed after $MaxRetries attempts: $Url"
    return $false
}
```

## 目录创建

### 确保目录存在
```powershell
function Ensure-Directory {
    param($Path)
    
    if (-not (Test-Path $Path)) {
        New-Item -ItemType Directory -Path $Path -Force | Out-Null
        Write-Host "Created directory: $Path"
    }
}

# 创建标准目录结构
$directories = @(
    "assets/images/backgrounds",
    "assets/images/logos",
    "assets/images/content",
    "assets/icons/ui",
    "assets/icons/social",
    "assets/audio/effects",
    "assets/audio/music",
    "assets/videos",
    "assets/fonts"
)

$directories | ForEach-Object { Ensure-Directory $_ }
```

## 完整工作流示例

```powershell
# 完整下载工作流
function Invoke-ResourceDownload {
    param(
        [string[]]$Urls,
        [string]$Type = "image",
        [string]$Category = "backgrounds",
        [string]$Prefix = "img-bg"
    )
    
    # 创建目录
    $outputDir = "assets/$Type/$Category"
    Ensure-Directory $outputDir
    
    # 下载文件
    $i = 1
    foreach ($url in $Urls) {
        $ext = [System.IO.Path]::GetExtension($url)
        if (-not $ext) { $ext = ".jpg" }
        
        $filename = "{0}-{1}-{2:D2}{3}" -f $Prefix, "downloaded", $i, $ext
        $outputPath = Join-Path $outputDir $filename
        
        if (Download-With-Retry -Url $url -Output $outputPath) {
            $i++
        }
    }
    
    # 更新清单
    New-ResourceManifest
    
    Write-Host "Download complete. Total files: $($i - 1)"
}
```
