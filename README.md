# Nice Components

一个基于 Vue 3 和 UnoCSS 构建的**复制即用**组件库，无需安装，复制代码即可使用！

## 🚀 核心理念：复制即用

**Nice Components** 不是传统的 npm 包，而是一个**开源的组件代码库**。您可以：

- 📋 **直接复制组件代码** - 点击组件的代码按钮，复制完整的 Vue 代码
- ⚡ **零配置使用** - 复制后直接粘贴到您的项目中即可使用
- 🎨 **自由定制** - 拥有完整源码，可随意修改样式和功能
- 📦 **无依赖负担** - 不会增加项目的依赖包体积

## ✨ 特性

- 🎨 **现代化设计** - 简约而不简单，符合现代 UI 设计趋势
- 📋 **复制即用** - 点击复制，粘贴使用，无需安装任何 npm 包
- 💪 **Vue 3 + Composition API** - 基于最新的 Vue 3 技术栈
- 🔧 **完全可定制** - 拥有源码，支持任意修改和扩展
- 📱 **响应式设计** - 完美适配各种屏幕尺寸
- 🌈 **UnoCSS 驱动** - 使用原子化 CSS，样式清晰易懂
- 🐳 **Docker 部署** - 支持容器化部署，开箱即用

## 🎯 组件列表

### 基础组件
- **Alert** - 警告提示组件
- **Badge** - 徽标组件
- **RippleButton** - 带涟漪效果的按钮组件

### 表单组件
- **Input** - 输入框组件
- **InputOTP** - OTP 验证码输入组件
- **Checkbox** - 复选框组件
- **Radio** - 单选框组件

### 导航组件
- **Pagination** - 滑块式分页组件
- **PaginationSimple** - 简单分页组件
- **PaginationDebug** - 调试分页组件
- **SliderTab** - 滑块标签页组件

### 反馈组件
- **Modal** - 模态框组件
- **Drawer** - 抽屉组件
- **Dropdown** - 下拉菜单组件

### 数据展示
- **Carousel** - 轮播图组件

### 系统组件
- **CodeModal** - 代码展示模态框
- **ParameterModal** - 参数说明模态框

> 💡 **提示**：每个组件都提供了完整的源码，您可以直接复制使用或根据需要进行修改。

## 🛠️ 技术栈

- **Vue 3** - 渐进式 JavaScript 框架
- **UnoCSS** - 即时原子化 CSS 引擎
- **Vite** - 下一代前端构建工具
- **Lucide Vue Next** - 图标库
- **Highlight.js** - 代码高亮
- **Docker** - 容器化部署支持

## 📋 如何使用组件

### 第一步：配置 UnoCSS

在您的项目中安装并配置 UnoCSS：

```bash
# 安装 UnoCSS
pnpm add -D unocss @unocss/preset-uno @unocss/preset-attributify @unocss/preset-icons

# 如果需要图标，还需要安装
pnpm add lucide-vue-next
```

在 `vite.config.js` 中配置：

```js
import UnoCSS from 'unocss/vite'

export default {
  plugins: [
    UnoCSS(),
    // ... 其他插件
  ],
}
```

创建 `uno.config.js`：

```js
import { defineConfig, presetUno, presetAttributify, presetIcons } from 'unocss'

export default defineConfig({
  presets: [
    presetUno(),
    presetAttributify(),
    presetIcons(),
  ],
})
```

### 第二步：复制组件代码

1. 🌐 **访问组件展示页面** - 启动本项目查看所有组件
2. 👁️ **预览组件效果** - 查看组件的各种状态和配置
3. 📋 **点击代码按钮** - 获取完整的组件源码
4. ✂️ **复制粘贴使用** - 直接粘贴到您的项目中

### 第三步：开始使用

```vue
<template>
  <div>
    <!-- 直接使用复制的组件 -->
    <Alert type="success" title="成功提示">
      这是一个成功提示消息
    </Alert>
    
    <RippleButton variant="primary" @click="handleClick">
      点击按钮
    </RippleButton>
  </div>
</template>

<script setup>
// 导入您复制的组件
import Alert from './components/Alert.vue'
import RippleButton from './components/RippleButton.vue'

const handleClick = () => {
  console.log('按钮被点击了！')
}
</script>
```

## 🎨 自定义和扩展

由于您拥有完整的组件源码，您可以：

- 🎨 **修改样式** - 直接编辑 UnoCSS 类名
- ⚙️ **调整功能** - 修改组件逻辑和交互
- 🔧 **添加属性** - 扩展组件的配置选项
- 🎯 **适配项目** - 完全按照项目需求定制

## 🚀 部署方式

### 🐳 Docker 部署（推荐）

**使用 Docker Compose（最简单）**

```bash
# 克隆项目
git clone https://github.com/nsmao-com/nice_unocss_components.git
cd nice_components

# 启动生产环境
docker-compose up -d

# 或启动开发环境
docker-compose --profile dev up -d
```

访问 `http://localhost:3000` 查看组件展示

**使用 Docker（手动构建）**

```bash
# 构建镜像
docker build -t nice-components .

# 运行容器
docker run -d \
  --name nice-components \
  -p 3000:80 \
  nice-components
```

**开发环境 Docker**

```bash
# 构建开发镜像
docker build -f Dockerfile.dev -t nice-components:dev .

# 运行开发容器
docker run -d \
  --name nice-components-dev \
  -p 5173:5173 \
  -v $(pwd):/app \
  -v /app/node_modules \
  nice-components:dev
```

### 📦 本地开发

如果您想本地运行这个展示项目：

```bash
# 克隆项目
git clone https://github.com/nsmao-com/nice_unocss_components.git

# 安装依赖
pnpm install

# 启动开发服务器
pnpm dev

# 构建生产版本
pnpm build

# 预览生产构建
pnpm preview
```

### ☁️ 云平台部署

**Vercel 部署**

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/nsmao-com/nice_unocss_components)

**Netlify 部署**

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/nsmao-com/nice_unocss_components)

**其他平台**

项目支持部署到任何支持静态网站的平台：
- GitHub Pages
- GitLab Pages  
- Firebase Hosting
- AWS S3 + CloudFront
- 阿里云 OSS
- 腾讯云 COS

## 🌟 IDE 推荐

- [VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) 
- 请禁用 Vetur 扩展以避免冲突

## 📄 相关文档

- [Vite 配置文档](https://vite.dev/config/)
- [UnoCSS 配置文档](https://uno.antfu.me/)
- [Vue 3 文档](https://vuejs.org/)
- [Docker 官方文档](https://docs.docker.com/)

## 💡 为什么选择复制即用？

相比传统的 npm 包组件库，复制即用的组件有以下优势：

- ✅ **完全控制** - 拥有源码，可任意修改
- ✅ **零依赖** - 不增加项目依赖负担
- ✅ **按需使用** - 只复制需要的组件
- ✅ **学习友好** - 可以学习组件实现原理
- ✅ **版本独立** - 不受组件库版本更新影响
- ✅ **快速部署** - 支持 Docker 一键部署

## 🛠️ 开发和生产环境

### 开发环境特性
- 🔥 **热重载** - 代码修改实时预览
- 🐛 **开发工具** - Vue DevTools 支持
- 📊 **性能监控** - Vite 开发服务器性能监控

### 生产环境特性
- ⚡ **静态资源优化** - Gzip 压缩，缓存策略
- 🔒 **安全头部** - 完整的安全响应头配置
- 🚀 **CDN 友好** - 静态资源适合 CDN 分发
- 📱 **PWA 就绪** - 可轻松扩展为 PWA 应用

## 🤝 贡献

欢迎提交 Pull Request 或 Issue 来帮助改进这个项目！

### 贡献指南
1. Fork 本项目
2. 创建您的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交您的更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开一个 Pull Request

## 📝 许可证

本项目采用 MIT 许可证，您可以自由使用、修改和分发。

## 🔗 相关链接

- **官网**: [奈斯猫](https://www.nsmao.com)
- **GitHub**: [nice_unocss_components](https://github.com/nsmao-com/nice_unocss_components)
- **在线演示**: [https://nice-components.nsmao.com](https://nice-components.nsmao.com)

---

*Made with ❤️ by [奈斯猫团队](https://www.nsmao.com)*

**💡 记住：不是安装，而是复制！这就是 Nice Components 的魅力所在。**
