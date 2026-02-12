# Resource Downloader Skill

自动从免费资源网站下载图片、音频、视频等资源的 Trae 技能包。

## 安装

### 方式一：使用 npx skillsadd（推荐）

```bash
npx skillsadd perwqaq/resource-downloader-skill
```

### 方式二：直接从 GitHub 克隆

```bash
# 克隆仓库
git clone https://github.com/perwqaq/resource-downloader-skill.git

# 复制到你的项目
cp -r resource-downloader-skill/skills/resource-downloader your-project/.trae/skills/
```

### 方式三：手动下载

1. 访问 [GitHub 仓库](https://github.com/perwqaq/resource-downloader-skill)
2. 点击 "Code" -> "Download ZIP"
3. 解压后将 `skills/resource-downloader` 目录复制到项目的 `.trae/skills/` 目录

```powershell
# Windows PowerShell
mkdir -p .trae\skills
Copy-Item -Recurse skills\resource-downloader .trae\skills\
```

```bash
# macOS/Linux
mkdir -p .trae/skills
cp -r skills/resource-downloader .trae/skills/
```

## 触发方式

当用户消息包含以下关键词时自动触发：

- "帮我下载"
- "下载资源"
- "需要图片"
- "需要音频"
- "找素材"
- "获取资源"

## 功能特性

- **智能资源搜索** - 根据需求自动选择合适的免费资源网站
- **多类型支持** - 图片、图标、音频、视频、字体、3D模型
- **规范命名** - 自动按项目规范重命名文件
- **目录组织** - 自动创建标准目录结构
- **许可记录** - 记录资源来源和许可证信息

## 支持的资源类型

| 类型 | 推荐格式 | 默认目录 |
|------|----------|----------|
| 图片 | png, jpg, svg, webp | assets/images/ |
| 图标 | svg, png | assets/icons/ |
| 音频 | mp3, wav, ogg | assets/audio/ |
| 视频 | mp4, webm | assets/videos/ |
| 字体 | ttf, woff, woff2 | assets/fonts/ |
| 3D模型 | glb, gltf | assets/models/ |

## 收录的免费资源网站

### 图片资源
- [Unsplash](https://unsplash.com) - 高质量摄影作品
- [Pexels](https://pexels.com) - 图片+视频，支持中文搜索
- [Pixabay](https://pixabay.com) - 图片+矢量图+视频

### 图标资源
- [Heroicons](https://heroicons.com) - Tailwind官方图标
- [Lucide](https://lucide.dev) - Feather Icons分支
- [Phosphor Icons](https://phosphoricons.com) - 灵活可定制

### 音频资源
- [Pixabay Music](https://pixabay.com/music) - 免费背景音乐
- [Freesound](https://freesound.org) - 用户上传音效库
- [Mixkit](https://mixkit.co/free-stock-music) - 音乐+音效

### 视频资源
- [Pexels Videos](https://pexels.com/videos) - 高质量视频片段
- [Coverr](https://coverr.co) - 网站背景视频
- [Mixkit](https://mixkit.co/free-stock-video) - 视频+音乐+模板

### 字体资源
- [Google Fonts](https://fonts.google.com) - 网页字体首选
- [Font Squirrel](https://fontsquirrel.com) - 商用免费字体

### 插画资源
- [unDraw](https://undraw.co) - 可定制配色SVG插画
- [Humaaans](https://humaaans.com) - 人物插画组合
- [Storyset](https://storyset.com) - 可定制场景插画

## 使用示例

```
用户: 帮我下载一些科技感的背景图片

助手会：
1. 确认需求（数量、风格等）
2. 从 Unsplash/Pexels 搜索
3. 下载到 assets/images/backgrounds/
4. 重命名为 img-bg-tech-01.jpg 等格式
5. 更新 resources-manifest.json
```

## 文件命名规范

### 基本格式
```
[类型前缀]-[类别]-[描述]-[序号].[扩展名]
```

### 示例
```
img-bg-hero-sunset-01.jpg
icon-ui-menu-hamburger.svg
audio-sfx-notification-success.mp3
video-intro-animation.webm
font-heading-bold.woff2
```

### 类型前缀
- `img-` 图片
- `icon-` 图标
- `audio-` 音频
- `video-` 视频
- `font-` 字体
- `model-` 3D模型

## 目录结构

```
project/
├── assets/
│   ├── images/
│   │   ├── backgrounds/
│   │   ├── logos/
│   │   └── content/
│   ├── icons/
│   │   ├── ui/
│   │   └── social/
│   ├── audio/
│   │   ├── effects/
│   │   └── music/
│   ├── videos/
│   └── fonts/
└── resources-manifest.json
```

## 技能文件结构

```
resource-downloader-skill/
├── README.md
├── package.json
└── skills/
    └── resource-downloader/
        ├── SKILL.md              # 主技能文件
        ├── resources.md          # 免费资源网站列表
        ├── naming-conventions.md # 文件命名规范
        └── scripts.md            # 下载脚本模板
```

## 注意事项

1. **版权合规** - 只下载明确标注可免费商用的资源
2. **许可记录** - 记录每个资源的来源和许可信息
3. **文件大小** - 注意控制资源文件大小，必要时进行压缩
4. **格式转换** - 根据项目需要转换格式

## 许可证

MIT License

## 贡献

欢迎提交 Issue 和 Pull Request！
