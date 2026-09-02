# GitHub Pages 部署指南

## 文件结构

```
github-pages/
├── index.html          # 主页面（纯 HTML 结构）
├── style.css           # 样式文件（独立 CSS）
├── config.json         # 数据配置（JSON 驱动）
└── assets/             # 图片资源文件夹
    ├── README.md       # 图片使用说明
    ├── avatar.png      # 头像
    ├── qrcode.png      # 公众号二维码
    ├── photo.jpg       # 摄影集封面
    ├── travel.jpg      # 旅行日记封面
    ├── coffee.jpg      # 咖啡时光封面
    ├── book.jpg        # 阅读清单封面
    ├── cocktail.jpg    # 调酒艺术封面
    ├── music.jpg       # 音乐收藏封面
    └── tea.jpg         # 茶道封面
```

## 部署步骤

### 1. 准备图片资源

将 9 张图片放入 `assets/` 文件夹（参考 `assets/README.md`）

### 2. 修改配置

编辑 `config.json`，根据你的需求修改：
- **profile**: 个人信息（名称、头像路径、微信号、B站链接等）
- **floatingTexts**: 漂浮文字内容、颜色、位置
- **sections**: Bento 模块的标题、描述、图片路径、链接等

### 3. 上传到 GitHub

#### 方式一：使用 GitHub 网页界面
1. 创建一个新的 GitHub 仓库
2. 点击 "Upload files"
3. 拖拽整个 `github-pages/` 文件夹的内容到上传区域
4. 提交 commit

#### 方式二：使用 Git 命令行
```bash
# 初始化 git（如果还没有）
cd github-pages
git init
git add .
git commit -m "Initial commit: Starry personal page"

# 关联远程仓库
git remote add origin https://github.com/你的用户名/仓库名.git
git branch -M main
git push -u origin main
```

### 4. 启用 GitHub Pages

1. 进入仓库的 **Settings** → **Pages**
2. 在 **Source** 下拉框选择 **Deploy from a branch**
3. 选择分支（通常是 `main` 或 `master`）
4. 文件夹选择 **/(root)**
5. 点击 **Save**

等待几分钟，GitHub Pages 会自动部署，你会看到一个绿色的提示显示访问地址。

### 5. 访问网站

部署成功后，访问地址格式为：
```
https://你的用户名.github.io/仓库名/
```

## 后续维护

### 修改内容

只需编辑 `config.json` 文件，无需修改 HTML 或 CSS：

```json
{
  "profile": {
    "name": "你的名字",
    "avatar": "assets/avatar.png",
    "wechatQrCode": "assets/qrcode.png",
    "wechatName": "你的微信号",
    "bilibiliUrl": "https://space.bilibili.com/你的ID"
  },
  // ... 其他配置
}
```

修改后提交到 GitHub，网站会自动更新。

### 更换图片

1. 替换 `assets/` 文件夹中的对应图片
2. 确保文件名与 `config.json` 中的一致
3. 提交到 GitHub

### 添加新模块

在 `config.json` 的 `sections` 数组中添加新的 module 对象：

```json
{
  "type": "square",
  "title": "新模块标题",
  "description": "模块描述",
  "image": "assets/new-image.jpg",
  "link": "https://example.com",
  "borderColor": "rgba(255,255,255,0.5)",
  "gradientFrom": "from-white-500",
  "gradientTo": "to-gray-500"
}
```

## 注意事项

1. **图片路径**: 所有图片路径必须是相对路径（如 `assets/avatar.png`），不能使用绝对路径
2. **文件大小**: GitHub Pages 单个文件限制 100MB，建议图片压缩后上传
3. **缓存问题**: 修改后如果看不到效果，尝试清除浏览器缓存或使用无痕模式
4. **自定义域名**: 可以在 GitHub Pages 设置中绑定自己的域名

## 技术特点

- **数据与视图分离**: 所有内容通过 `config.json` 驱动，修改配置即可更新页面
- **零依赖**: 纯 HTML/CSS/JavaScript，无需构建工具
- **响应式设计**: 自动适配 PC 和移动端
- **动画效果**: CSS keyframes 实现漂浮星球、漂浮文字等动效
- **模块化布局**: Bento Grid 网格系统，支持横向/竖向/正方形三种模块类型
