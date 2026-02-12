# 文件命名规范

本文档定义资源文件的命名规范，确保项目资源的一致性和可维护性。

## 命名模板

### 基本格式
```
[类型前缀]-[类别]-[描述]-[变体/序号].[扩展名]
```

### 示例
```
img-bg-hero-sunset-01.jpg
icon-ui-menu-hamburger.svg
audio-sfx-notification-success.mp3
```

## 类型前缀

| 前缀 | 类型 | 示例 |
|------|------|------|
| `img-` | 图片 | img-bg-homepage.jpg |
| `icon-` | 图标 | icon-social-twitter.svg |
| `audio-` | 音频 | audio-music-ambient.mp3 |
| `video-` | 视频 | video-intro-product.mp4 |
| `font-` | 字体 | font-heading-bold.woff2 |
| `model-` | 3D模型 | model-character-hero.glb |

## 类别分类

### 图片类别

| 类别 | 用途 | 示例 |
|------|------|------|
| `bg` | 背景图 | img-bg-gradient-01.jpg |
| `hero` | 首页大图 | img-hero-main.jpg |
| `banner` | 横幅图片 | img-banner-promo.png |
| `logo` | 品牌Logo | img-logo-primary.svg |
| `avatar` | 用户头像 | img-avatar-default.png |
| `thumb` | 缩略图 | img-thumb-product-01.jpg |
| `content` | 内容配图 | img-content-article-01.jpg |
| `illustration` | 插画 | img-illustration-empty.svg |
| `photo` | 照片 | img-photo-team-01.jpg |

### 图标类别

| 类别 | 用途 | 示例 |
|------|------|------|
| `ui` | 界面图标 | icon-ui-close.svg |
| `social` | 社交媒体 | icon-social-wechat.svg |
| `arrow` | 箭头图标 | icon-arrow-right.svg |
| `action` | 操作图标 | icon-action-delete.svg |
| `status` | 状态图标 | icon-status-success.svg |
| `file` | 文件图标 | icon-file-pdf.svg |
| `brand` | 品牌图标 | icon-brand-apple.svg |

### 音频类别

| 类别 | 用途 | 示例 |
|------|------|------|
| `sfx` | 音效 | audio-sfx-click.mp3 |
| `music` | 音乐 | audio-music-background.mp3 |
| `voice` | 语音 | audio-voice-welcome.mp3 |
| `ambient` | 环境音 | audio-ambient-rain.mp3 |

### 视频类别

| 类别 | 用途 | 示例 |
|------|------|------|
| `intro` | 开场视频 | video-intro-brand.mp4 |
| `tutorial` | 教程视频 | video-tutorial-setup.mp4 |
| `promo` | 宣传视频 | video-promo-feature.mp4 |
| `loop` | 循环视频 | video-loop-background.mp4 |

## 描述命名规则

### 命名原则

1. **使用英文**：便于跨平台兼容
2. **小写字母**：全部小写，避免大小写混乱
3. **连字符分隔**：使用 `-` 连接单词
4. **描述性强**：名称应体现内容或用途
5. **避免缩写**：除非是通用缩写（如 bg, sfx）

### 常用描述词

| 中文 | 英文 | 示例 |
|------|------|------|
| 主要 | main, primary | img-hero-primary.jpg |
| 次要 | secondary | img-bg-secondary.jpg |
| 默认 | default | img-avatar-default.png |
| 激活 | active | icon-tab-active.svg |
| 禁用 | disabled | icon-btn-disabled.svg |
| 悬停 | hover | icon-btn-hover.svg |
| 选中 | selected | icon-checkbox-selected.svg |
| 错误 | error | icon-status-error.svg |
| 成功 | success | icon-status-success.svg |
| 警告 | warning | icon-status-warning.svg |

## 变体与序号

### 状态变体
```
icon-btn-primary.svg
icon-btn-primary-hover.svg
icon-btn-primary-active.svg
icon-btn-primary-disabled.svg
```

### 尺寸变体
```
img-logo-small.png
img-logo-medium.png
img-logo-large.png
```

### 序号规则
```
img-gallery-01.jpg
img-gallery-02.jpg
img-gallery-03.jpg
```

## 特殊情况处理

### 主题系列
```
img-bg-tech-circuit-01.jpg
img-bg-tech-network-02.jpg
img-bg-tech-digital-03.jpg
```

### 多语言版本
```
img-banner-promo-en.jpg
img-banner-promo-zh.jpg
img-banner-promo-ja.jpg
```

### 深色/浅色模式
```
img-bg-home-light.jpg
img-bg-home-dark.jpg
```

## 目录组织

### 按类型组织
```
assets/
├── images/
│   ├── backgrounds/
│   ├── logos/
│   ├── heroes/
│   └── content/
├── icons/
│   ├── ui/
│   ├── social/
│   └── brand/
└── audio/
    ├── effects/
    └── music/
```

### 按功能组织
```
assets/
├── common/          # 通用资源
├── home/            # 首页资源
├── about/           # 关于页面
└── products/        # 产品页面
```

## 命名检查清单

在命名文件时，请确认：

- [ ] 使用了正确的类型前缀
- [ ] 类别描述准确
- [ ] 全部小写字母
- [ ] 使用连字符分隔
- [ ] 无空格和特殊字符
- [ ] 文件扩展名正确
- [ ] 名称具有描述性
- [ ] 遵循项目现有命名风格

## 批量重命名示例

### PowerShell
```powershell
# 批量添加前缀
Get-ChildItem *.jpg | ForEach-Object { Rename-Item $_ -NewName "img-$($_.Name)" }

# 批量替换空格为连字符
Get-ChildItem * | Rename-Item -NewName { $_.Name -replace ' ', '-' }
```

### 批量下载时自动命名
```powershell
$i = 1
$urls | ForEach-Object {
    $filename = "img-bg-tech-{0:D2}.jpg" -f $i
    Invoke-WebRequest -Uri $_ -OutFile $filename
    $i++
}
```
