# Vue3 全栈开发实战深度教学手册 - 小白保姆级 (完整版)

> 🎓 **适用人群**：零基础小白、计算机专业学生、前端初学者
> 💡 **教程目标**：手把手教你从零开始，搭建一个企业级的「个人视频管理系统」。不仅教你怎么写代码，更教你为什么要这么写。
> 🛠 **核心技术**：Vue 3 + Vite + Element Plus + ECharts + Pinia
> 📅 **最后更新**：2025-12-15

---

## 📚 目录导航

1.  [第一章：项目起步与环境搭建](#第一章项目起步与环境搭建)
    *   1.1 Node.js 环境安装与配置
    *   1.2 使用 Vite 快速初始化项目
    *   1.3 项目目录结构深度解析
    *   1.4 安装企业级开发全家桶
2.  [第二章：Vue3 核心概念与组件化思维](#第二章vue3-核心概念与组件化思维)
    *   2.1 抛弃 Options API，拥抱 Composition API
    *   2.2 `setup` 语法糖详解
    *   2.3 响应式原理：`ref` vs `reactive` (深度解析)
    *   2.4 组件通信的三种姿势
    *   2.5 生命周期钩子函数详解
3.  [第三章：构建用户认证系统 (Login/Register)](#第三章构建用户认证系统-loginregister)
    *   3.1 登录页面的布局实现
    *   3.2 表单验证规则 (`rules`) 的编写
    *   3.3 本地存储实战：`localStorage` 模拟数据库
    *   3.4 路由守卫：防止未登录用户访问后台
4.  [第四章：系统布局与导航设计](#第四章系统布局与导航设计)
    *   4.1 Element Plus 容器布局 (`el-container`)
    *   4.2 侧边栏菜单 (`el-menu`) 的递归实现
    *   4.3 头部组件与面包屑导航
    *   4.4 嵌套路由 (`children`) 的配置技巧
5.  [第五章：核心业务 - 视频管理系统](#第五章核心业务---视频管理系统)
    *   5.1 表格组件 (`el-table`) 的深度使用
    *   5.2 分页器 (`el-pagination`) 的逻辑实现
    *   5.3 **亮点功能**：基于 `computed` 的零延迟实时搜索
    *   5.4 **核心难点**：纯前端导出 CSV 文件 (Blob 原理)
    *   5.5 批量删除与二次确认 (`ElMessageBox`)
6.  [第六章：数据可视化与 ECharts 集成](#第六章数据可视化与-echarts-集成)
    *   6.1 ECharts 基础配置与按需引入
    *   6.2 柱状图与折线图的动态渲染
    *   6.3 响应式图表：随窗口大小自动缩放
    *   6.4 异步数据加载与 Loading 状态
7.  [第七章：个人中心与数据持久化](#第七章个人中心与数据持久化)
    *   7.1 头像上传原理：Base64 vs Blob URL
    *   7.2 解决“串号”问题：用户数据的隔离策略
    *   7.3 密码修改与二次验证逻辑
8.  [第八章：项目优化、打包与常见问题](#第八章项目优化打包与常见问题)
    *   8.1 代码规范：ESLint + Prettier
    *   8.2 性能优化：路由懒加载与组件异步加载
    *   8.3 Vite 打包配置与生产环境部署
    *   8.4 常见报错 (404, CORS) 及其解决方案
9.  [附录：Vue3 面试高频考点](#附录vue3-面试高频考点)

---

## 第一章：项目起步与环境搭建

### 1.1 Node.js 环境安装与配置

在开始任何前端项目之前，你需要一个运行环境。Node.js 就是前端的“发动机”。它让 JavaScript 能够脱离浏览器，在服务器或本地电脑上运行。

**安装步骤：**
1.  **下载**：访问 [Node.js 官网](https://nodejs.org/)，下载 **LTS (长期支持版)**。不要下载 Current 版本，那个不稳定。
2.  **安装**：一路点击 "Next" 即可。默认安装路径是 `C:\Program Files\nodejs`，建议不要改。
3.  **验证**：打开终端 (Win+R 输入 cmd)，输入以下命令：
    ```bash
    node -v
    # 输出示例: v16.14.0 (只要大于 v14 即可)

    npm -v
    # 输出示例: 8.3.1 (npm 是随 node 一起安装的包管理器)
    ```
4.  **配置淘宝镜像** (国内加速下载)：
    默认的 npm 源在国外，下载很慢。我们把它切换到国内的淘宝镜像。
    ```bash
    npm config set registry https://registry.npmmirror.com
    
    # 验证是否成功
    npm config get registry
    # 输出应该包含 npmmirror.com
    ```

### 1.2 使用 Vite 快速初始化项目

Vite (法语意为"快") 是新一代的前端构建工具。它比传统的 Webpack 快 10-100 倍。

```bash
# 1. 创建项目 (项目名: vue_video_manage)
# --template vue 表示直接使用 Vue 模板，不问问题
npm create vite@latest vue_video_manage -- --template vue

# 2. 进入项目目录
cd vue_video_manage

# 3. 安装依赖 (下载 node_modules)
# 这一步会根据 package.json 下载所有需要的库
npm install

# 4. 启动项目
npm run dev
```

启动后，你会看到终端显示 `Local: http://127.0.0.1:5173/`。按住 Ctrl 点击链接，在浏览器打开它。恭喜你，你的第一个 Vue3 项目跑起来了！

### 1.3 项目目录结构深度解析

一个标准的 Vue3 项目结构如下，一定要熟悉每个文件的作用：

```
vue_video_manage/
├── .vscode/             # VSCode 编辑器配置 (可选)
├── node_modules/        # 依赖包目录 (不要动它，体积很大)
├── public/              # 静态资源 (不会被打包工具处理，直接复制到根目录)
│   └── favicon.ico      # 网站图标
├── src/                 # 源代码目录 (我们99%的工作都在这里)
│   ├── assets/          # 静态资源 (会被打包处理，如图片、CSS、字体)
│   ├── components/      # 公共组件 (如头部、侧边栏、按钮)
│   ├── router/          # 路由配置 (页面跳转逻辑)
│   ├── stores/          # 状态管理 (Pinia)
│   ├── utils/           # 工具函数 (如日期格式化、请求封装)
│   ├── views/           # 页面组件 (如登录页、首页、404页)
│   ├── App.vue          # 根组件 (所有页面的入口，像一个相框)
│   └── main.js          # 入口文件 (挂载 Vue 实例，配置全局插件)
├── .gitignore           # Git 忽略文件配置
├── index.html           # HTML 模板 (Vite 项目的入口是 index.html，不是 main.js)
├── package.json         # 项目配置文件 (依赖列表、启动脚本)
├── README.md            # 项目说明文档
└── vite.config.js       # Vite 配置文件 (配置代理、别名等)
```

### 1.4 安装企业级开发全家桶

为了开发一个功能完整的系统，我们需要安装以下核心库。每个库都有它的使命：

```bash
# 1. 路由管理 (Vue Router)
# 用于实现单页应用 (SPA) 的页面跳转，不刷新页面
npm install vue-router@4

# 2. 状态管理 (Pinia - 替代 Vuex)
# 用于跨组件共享数据 (比如用户信息、购物车数据)
npm install pinia

# 3. UI 组件库 (Element Plus)
# 提供现成的按钮、表格、弹窗，不用自己写 CSS
npm install element-plus

# 4. 图标库
# Element Plus 配套的图标集合
npm install @element-plus/icons-vue

# 5. CSS 预处理器 (Sass)
# 让 CSS 写起来更方便 (支持嵌套、变量)
# -D 表示只在开发环境使用
npm install sass -D

# 6. 图表库 (ECharts)
# 用于画折线图、柱状图
npm install echarts

# 7. 网络请求 (Axios)
# 用于向后端发送 HTTP 请求
npm install axios
```

**配置 `main.js` 全局引入 Element Plus：**

```javascript
// src/main.js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css' // 引入 Element Plus 的样式文件
import * as ElementPlusIconsVue from '@element-plus/icons-vue' // 引入所有图标
import App from './App.vue'
import router from './router'

const app = createApp(App)

// 注册所有图标
// 这样在任何组件里都可以直接使用 <Edit /> 或 <User />
for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
  app.component(key, component)
}

app.use(createPinia()) // 启用 Pinia
app.use(router)        // 启用路由
app.use(ElementPlus)   // 启用 Element Plus

app.mount('#app')      // 挂载到 index.html 的 #app 节点上
```

---

## 第二章：Vue3 核心概念与组件化思维

### 2.1 抛弃 Options API，拥抱 Composition API

**背景故事**：
在 Vue 2 时代，我们写代码像“填空题”。数据必须填在 `data()` 里，方法必须填在 `methods()` 里，计算属性填在 `computed()` 里。
*   **痛点**：当一个组件有 500 行代码时，为了修改一个“搜索功能”，你可能需要在 data（第 10 行）、methods（第 400 行）和 created（第 200 行）之间反复上下滚动，非常痛苦。这叫“反复横跳”。

**Vue 3 的革命**：
Vue 3 引入了 **Composition API (组合式 API)**，允许我们像写普通 JavaScript 函数一样，把同一个功能的代码（数据+方法+生命周期）写在一起。
*   **优势**：代码组织更紧凑，逻辑更清晰，复用更简单。

### 2.2 `setup` 语法糖详解

`<script setup>` 是 Vue 3 给我们的一颗“糖”，让代码写起来更甜（简洁）。

**传统写法 vs Setup 语法糖**：

| 特性 | 传统 `export default` | `<script setup>` |
| :--- | :--- | :--- |
| **代码量** | 啰嗦，需要 `return` 暴露变量 | **极简**，定义的变量模板直接可用 |
| **组件注册** | 需要 `components: { Child }` | 引入即可用 `import Child from ...` |
| **性能** | 运行时编译 | **编译时优化**，运行更快 |
| **this** | 有 `this` 指向问题 | **没有 `this`**，函数式编程 |

**代码对比：**

```vue
<!-- 😭 Vue 2 / 传统 Vue 3 写法 -->
<script>
export default {
  data() {
    return { count: 0 }
  },
  methods: {
    add() { this.count++ }
  }
}
</script>

<!-- 😍 Vue 3 setup 语法糖 (本项目采用) -->
<script setup>
import { ref } from 'vue'

// 就像写普通 JS 一样自然
const count = ref(0)
const add = () => count.value++
</script>
```

### 2.3 响应式原理：`ref` vs `reactive`

这是新手最容易晕的地方，我们用**“生活案例”**来理解。

#### 1. `ref` (万能钥匙)
*   **适用场景**：基本类型（数字、字符串、布尔值），也可以包对象。
*   **原理**：它像一个**“盒子”**。你给它一个数字 `0`，它给你包装成一个对象 `{ value: 0 }`。Vue 监听这个盒子的 `.value` 属性。
*   **使用规则**：
    *   在 `<script>` 里：必须加 `.value` 才能拿到里面的东西。（比如 `count.value`）
    *   在 `<template>` 里：**不需要**加 `.value`，Vue 帮你拆开了。

```javascript
const name = ref('Jack')
console.log(name)       // RefImpl 对象
console.log(name.value) // 'Jack' (拿到真值)

// 修改值
name.value = 'Rose'
```

#### 2. `reactive` (对象专家)
*   **适用场景**：只能放**对象**或**数组**。
*   **原理**：基于 ES6 的 `Proxy`（代理）。就像给对象请了个“管家”，你读写属性时，管家都会拦截并通知视图更新。
*   **使用规则**：不需要 `.value`，像普通对象一样用。
*   **大坑**：**不能直接解构**，也不能直接重新赋值（会丢失响应性）。

```javascript
const user = reactive({ name: 'Jack', age: 18 })
console.log(user.name) // 'Jack' (直接拿)

// ❌ 错误用法1：直接解构会失去响应性
// let { name } = user 

// ❌ 错误用法2：直接替换整个对象
// user = { name: 'Rose' } // 响应性丢失
```

#### 💡 最佳实践 (新手必看)
为了减少心智负担，**建议 99% 的情况都用 `ref`**。
*   基本类型用 `ref`。
*   对象也可以用 `ref` (内部会自动转 reactive)。
*   只有在处理极其复杂的表单对象时，才考虑 `reactive`。

### 2.4 组件通信的三种姿势

组件之间怎么传数据？就像人与人之间怎么聊天。

#### 1. 父传子 (`defineProps`) —— 就像“爸爸给儿子零花钱”
*   **方向**：单向数据流（父 -> 子）。
*   **规则**：儿子只能用，不能改（改了会报错）。这叫“单向数据流”，为了防止数据混乱。

```vue
<!-- 👨 父组件 (Father.vue) -->
<template>
  <!-- 把 money 传给 Son -->
  <Son :money="100" task="写作业" />
</template>

<!-- 👦 子组件 (Son.vue) -->
<script setup>
// 接收 props
// defineProps 不需要引入，直接用
const props = defineProps({
  money: Number,
  task: String
})
console.log(`爸爸给了我 ${props.money} 元，让我 ${props.task}`)
</script>
```

#### 2. 子传父 (`defineEmits`) —— 就像“儿子给爸爸汇报成绩”
*   **方向**：子组件触发事件 -> 父组件监听。

```vue
<!-- 👦 子组件 (Son.vue) -->
<script setup>
// 定义有哪些事件可以发
const emit = defineEmits(['finish'])

const doHomework = () => {
  // 干完活了，通知爸爸，并传回结果
  emit('finish', '作业做完了！')
}
</script>

<!-- 👨 父组件 (Father.vue) -->
<template>
  <!-- 监听 finish 事件 -->
  <Son @finish="handleFinish" />
</template>

<script setup>
const handleFinish = (msg) => {
  console.log('收到儿子的消息：', msg)
}
</script>
```

#### 3. 全局状态管理 (Pinia) —— 就像“家庭留言板”
*   **场景**：当组件 A 和组件 Z 隔了十万八千里，或者多个组件都要用同一份数据（比如**用户信息**）。
*   **Pinia**：Vue 官方推荐的状态管理库，比 Vuex 更简单，更轻量。

```javascript
// src/stores/user.js (定义 Store)
import { defineStore } from 'pinia'
import { ref } from 'vue'

export const useUserStore = defineStore('user', () => {
  // State (数据)
  const userInfo = ref({})
  
  // Actions (方法)
  const setUser = (data) => {
    userInfo.value = data
  }

  // Getters (计算属性 - 可选)
  // const isLoggedIn = computed(() => !!userInfo.value.token)

  return { userInfo, setUser }
})
```

**在组件中使用 Pinia：**

```vue
<script setup>
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

// 读取数据
console.log(userStore.userInfo)

// 修改数据
userStore.setUser({ name: 'Admin' })
</script>
```

### 2.5 生命周期钩子函数详解

Vue 组件从创建到销毁会经历一系列过程，这些过程中的回调函数叫“生命周期钩子”。

*   `onMounted`: **最常用**。组件挂载完成后执行。适合**发请求**、**操作 DOM**、**初始化图表**。
*   `onUpdated`: 组件数据更新，DOM 重新渲染后执行。
*   `onUnmounted`: 组件销毁前执行。适合**清除定时器**、**解绑事件监听**。

```javascript
import { onMounted, onUnmounted } from 'vue'

onMounted(() => {
  console.log('组件加载完毕，可以发请求了')
})

onUnmounted(() => {
  console.log('组件要死了，清理后事')
})
```

---

## 第三章：构建用户认证系统 (Login/Register)

### 3.1 登录页面的布局实现

我们使用 Element Plus 的 `el-form` 组件，它帮我们处理了布局、对齐和校验，非常方便。

**关键代码结构 (`src/views/Login.vue`)：**

```vue
<template>
  <div class="login-wrap">
    <!-- model: 绑定表单数据对象 -->
    <!-- rules: 绑定验证规则 -->
    <!-- ref: 给表单起个名，方便 JS 里调用它 -->
    <el-form :model="form" :rules="rules" ref="formRef" class="login-box">
      <h3 class="title">系统登录</h3>
      
      <!-- prop: 对应 rules 里的规则名 -->
      <el-form-item prop="username">
        <el-input v-model="form.username" placeholder="请输入账号" :prefix-icon="User" />
      </el-form-item>
      
      <el-form-item prop="password">
        <el-input 
          type="password" 
          v-model="form.password" 
          placeholder="请输入密码" 
          show-password 
          :prefix-icon="Lock" 
        />
      </el-form-item>
      
      <el-button type="primary" class="login-btn" @click="handleLogin">登录</el-button>
    </el-form>
  </div>
</template>

<style scoped>
.login-wrap {
  width: 100vw;
  height: 100vh;
  background: #2d3a4b; /* 深色背景 */
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-box {
  width: 400px;
  padding: 40px;
  background: #fff;
  border-radius: 10px;
}
</style>
```

### 3.2 表单验证规则 (`rules`) 的编写

验证是保证数据质量的第一道防线。Element Plus 使用 `async-validator` 库。

```javascript
// 定义响应式表单数据
const form = reactive({
  username: '',
  password: ''
})

// 定义验证规则
const rules = reactive({
  username: [
    // required: 必填, message: 错误提示, trigger: 触发时机(blur=失去焦点)
    { required: true, message: '请输入用户名', trigger: 'blur' },
    { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
  ],
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' }
  ]
})
```

### 3.3 本地存储实战：`localStorage` 模拟数据库

**背景**：因为本项目是纯前端演示，没有真实的后端服务器。
**方案**：我们使用浏览器的 `localStorage` 来充当“微型数据库”。它能把数据存在用户的浏览器里，关闭页面也不会丢失。

**核心 API**：
*   `localStorage.setItem('key', 'value')`: 存数据（必须是字符串）
*   `localStorage.getItem('key')`: 取数据
*   `JSON.stringify(obj)`: 对象转字符串
*   `JSON.parse(str)`: 字符串转对象

**注册逻辑 (存数据)：**
```javascript
const register = () => {
  const userData = { username: form.username, password: form.password }
  // 把对象转成字符串存进去
  localStorage.setItem('registerForm', JSON.stringify(userData))
  ElMessage.success('注册成功，请去登录')
}
```

**登录逻辑 (取数据比对)：**
```javascript
const login = () => {
  // 1. 先验证表单格式对不对
  formRef.value.validate((valid) => {
    if (valid) {
      // 2. 取出注册的数据
      const localUserStr = localStorage.getItem('registerForm')
      
      if (!localUserStr) {
        return ElMessage.error('请先注册账号')
      }
      
      const localUser = JSON.parse(localUserStr)
      
      // 3. 比对账号密码
      if (form.username === localUser.username && form.password === localUser.password) {
        // 4. 登录成功，保存一个“令牌” (userInfo) 证明我登录过了
        localStorage.setItem('userInfo', JSON.stringify(localUser))
        router.push('/main') // 跳转到主页
      } else {
        ElMessage.error('账号或密码错误')
      }
    }
  })
}
```

### 3.4 路由守卫：防止未登录用户访问后台

**问题**：如果用户直接在浏览器地址栏输入 `http://localhost:5173/main`，即便没登录也能进去，这不安全。
**解决**：使用 Vue Router 的 **全局前置守卫 (`beforeEach`)**。就像小区的门卫，进门前先查证。

**`src/router/index.js`：**

```javascript
// to: 要去哪里
// from: 从哪里来
// next: 放行函数
router.beforeEach((to, from, next) => {
  // 1. 获取登录状态 (看看口袋里有没有 userInfo 这个证件)
  const isAuthenticated = localStorage.getItem('userInfo')
  
  // 2. 判断逻辑
  // 如果要去的地方不是登录页，且没有证件
  if (to.path !== '/login' && !isAuthenticated) {
    next('/login') // 滚回去登录
  } else {
    next() // 证件齐全，请进
  }
})
```

---

## 第四章：系统布局与导航设计

### 4.1 Element Plus 容器布局

后台管理系统通常采用经典的 **"左侧菜单 + 顶部头部 + 内容区域"** 布局。
我们使用 `el-container`, `el-header`, `el-aside`, `el-main` 这几个组件来搭建骨架。

```vue
<!-- src/views/MainIndex.vue -->
<template>
  <el-container class="layout-container">
    <!-- 左侧边栏：放导航菜单 -->
    <el-aside width="200px">
      <LeftNav />
    </el-aside>
    
    <el-container>
      <!-- 顶部头部：放面包屑、个人头像 -->
      <el-header>
        <SysHeader />
      </el-header>
      
      <!-- 内容区域：这是最关键的！ -->
      <!-- router-view 是一个占位符，不同的页面内容会显示在这里 -->
      <el-main>
        <router-view />
      </el-main>
    </el-container>
  </el-container>
</template>
```

### 4.2 侧边栏菜单 (`el-menu`) 的递归实现

Element Plus 的菜单组件支持 `router` 模式，开启后，点击菜单会自动跳转到 `index` 属性指定的路由。

```vue
<!-- :default-active="$route.path" 让菜单高亮自动跟随当前路由 -->
<el-menu 
  router 
  :default-active="$route.path"
  background-color="#304156"
  text-color="#fff"
>
  <!-- 子菜单 (有下拉) -->
  <el-sub-menu index="/video">
    <template #title>
      <el-icon><VideoCamera /></el-icon>
      <span>视频管理</span>
    </template>
    <!-- index 就是要跳转的路径 -->
    <el-menu-item index="/video/manage">视频列表</el-menu-item>
  </el-sub-menu>
  
  <!-- 普通菜单 (无下拉) -->
  <el-menu-item index="/self/info">
    <el-icon><User /></el-icon>
    <span>个人中心</span>
  </el-menu-item>
</el-menu>
```

### 4.3 头部组件与面包屑导航

头部通常包含面包屑导航 (Breadcrumb) 和用户下拉菜单。

```vue
<!-- SysHeader.vue -->
<div class="header-right">
  <el-dropdown>
    <span class="el-dropdown-link">
      {{ username }}
      <el-icon class="el-icon--right"><arrow-down /></el-icon>
    </span>
    <template #dropdown>
      <el-dropdown-menu>
        <el-dropdown-item @click="logout">退出登录</el-dropdown-item>
      </el-dropdown-menu>
    </template>
  </el-dropdown>
</div>
```

### 4.4 嵌套路由 (`children`) 的配置技巧

Vue Router 的嵌套路由允许我们在父组件中渲染子组件。

```javascript
// router/index.js
{
  path: '/main',
  component: MainIndex, // 父组件 (布局框架)
  redirect: '/video/manage',
  children: [
    {
      path: 'video/manage', // 注意：子路由路径不要加 /
      component: VideoManage
    },
    {
      path: 'self/info',
      component: SelfInfo
    }
  ]
}
```

---

## 第五章：核心业务 - 视频管理系统

这是全系统含金量最高的部分，集成了增删改查、搜索、分页、导出等功能。

### 5.1 表格组件 (`el-table`) 的深度使用

```vue
<!-- :data 绑定当前页的数据 -->
<el-table :data="currentPageData" border stripe>
  <!-- prop 对应数据对象里的 key -->
  <el-table-column prop="id" label="ID" width="80" />
  <el-table-column prop="title" label="视频标题" />
  
  <!-- 自定义列模板：比如显示图片 -->
  <el-table-column prop="cover" label="封面">
    <template #default="scope">
      <!-- scope.row 就是当前这一行的数据对象 -->
      <img :src="scope.row.cover" style="width: 50px; border-radius: 4px;" />
    </template>
  </el-table-column>
  
  <el-table-column label="操作" width="180">
    <template #default="scope">
      <el-button size="small" @click="handleEdit(scope.row)">编辑</el-button>
      <el-button size="small" type="danger" @click="handleDelete(scope.row)">删除</el-button>
    </template>
  </el-table-column>
</el-table>
```

### 5.2 分页器 (`el-pagination`) 的逻辑实现

前端分页的核心思想是：**利用数组的 `slice` 方法进行切片**。
假设有 100 条数据，每页 10 条。
*   第 1 页：取索引 0~9
*   第 2 页：取索引 10~19

```javascript
// 分页配置
const page = reactive({
  current: 1, // 当前页码
  size: 10,   // 每页条数
  total: 0    // 总条数
})

// 计算属性：自动计算当前页应该显示哪些数据
const currentPageData = computed(() => {
  // 1. 先从所有数据中筛选出符合搜索条件的 (filteredData)
  // 2. 再计算切片的起始位置
  const start = (page.current - 1) * page.size
  const end = start + page.size
  
  // 3. 切割数组
  return filteredData.value.slice(start, end)
})

// 翻页事件
const handleCurrentChange = (val) => {
  page.current = val
}
```

### 5.3 亮点功能：基于 `computed` 的零延迟实时搜索

**面试加分项**：传统的搜索是用户输入 -> 点击搜索按钮 -> 发送 API 请求 -> 刷新表格。
我们的搜索是：**用户每敲一个字母，表格自动更新**。

**原理**：利用 Vue 的 `computed` 计算属性的依赖追踪特性。

```javascript
const searchKeyword = ref('') // 搜索框绑定的变量
const videoType = ref('')     // 下拉框绑定的变量

// 这里的 filteredData 就是表格真正的数据源
const filteredData = computed(() => {
  // tableData.value 是所有的原始数据
  return tableData.value.filter(item => {
    // 1. 标题包含关键词 (如果没有输入关键词，includes 返回 true)
    const matchTitle = !searchKeyword.value || item.title.includes(searchKeyword.value)
    
    // 2. 类型匹配 (如果没选类型，则默认匹配所有)
    const matchType = !videoType.value || item.type === videoType.value
    
    // 必须同时满足两个条件
    return matchTitle && matchType
  })
})
```

### 5.4 核心难点：纯前端导出 CSV 文件 (Blob 原理)

**场景**：用户想把表格数据下载到 Excel 里看。通常这需要后端生成文件，但我们用纯前端也能做！

**比喻**：
1.  **切菜 (map)**：把原始数据里的英文 key (`title`) 换成中文表头 (`视频标题`)。
2.  **装盒 (join)**：把数据拼成 CSV 格式的字符串（逗号分隔）。
3.  **密封 (Blob)**：把字符串封装成一个二进制对象，假装它是一个文件。
4.  **发货 (URL)**：给这个对象生成一个临时的下载链接，模拟点击。

**代码实现：**

```javascript
const exportData = () => {
  // 1. 数据清洗
  const data = filteredData.value.map(item => ({
    '视频ID': item.id,
    '视频标题': item.title,
    '发布时间': item.date
  }))

  // 2. 生成 CSV 字符串
  // Object.keys 拿表头: "视频ID,视频标题,发布时间"
  const header = Object.keys(data[0]).join(',')
  // Object.values 拿内容: "1,测试视频,2023-01-01"
  const content = data.map(row => Object.values(row).join(',')).join('\n')
  const csvString = `${header}\n${content}`

  // 3. 封装为 Blob 对象 (重要！)
  // \uFEFF 是 BOM 头，解决 Excel 打开中文乱码问题
  const blob = new Blob(['\uFEFF' + csvString], { type: 'text/csv;charset=utf-8' })

  // 4. 创建临时的下载链接
  const link = document.createElement('a')
  link.href = URL.createObjectURL(blob) // 生成 blob:http://... 链接
  link.download = `视频数据_${new Date().getTime()}.csv`
  
  // 5. 模拟点击触发下载
  link.click()
  
  // 6. 垃圾回收：释放内存
  URL.revokeObjectURL(link.href)
}
```

### 5.5 批量删除与二次确认 (`ElMessageBox`)

安全操作必须有二次确认。

```javascript
const handleDelete = (row) => {
  ElMessageBox.confirm(
    '确定要删除这条数据吗？此操作不可恢复！',
    '警告',
    {
      confirmButtonText: '确定删除',
      cancelButtonText: '取消',
      type: 'warning',
    }
  )
  .then(() => {
    // 用户点了确定
    const index = tableData.value.findIndex(item => item.id === row.id)
    tableData.value.splice(index, 1)
    ElMessage.success('删除成功')
  })
  .catch(() => {
    // 用户点了取消
    ElMessage.info('已取消删除')
  })
}
```

---

## 第六章：数据可视化与 ECharts 集成

### 6.1 ECharts 基础配置与按需引入

**安装**：`npm install echarts`

**核心步骤**：
1.  准备一个有宽高的 DOM 容器 (`div`)。
2.  `echarts.init` 初始化实例。
3.  `setOption` 设置图表数据。

```vue
<template>
  <!-- 必须给容器指定高度，否则图表不显示！ -->
  <div ref="chartRef" style="width: 100%; height: 400px;"></div>
</template>

<script setup>
import * as echarts from 'echarts'
import { ref, onMounted } from 'vue'

const chartRef = ref(null) // 拿到 DOM 元素

// 必须在 onMounted 里初始化，因为这时候 DOM 才渲染完
onMounted(() => {
  const myChart = echarts.init(chartRef.value)
  
  const option = {
    title: { text: '播放量趋势' },
    tooltip: { trigger: 'axis' },
    xAxis: { type: 'category', data: ['周一', '周二', '周三'] },
    yAxis: { type: 'value' },
    series: [{ 
      data: [120, 200, 150], 
      type: 'line', // line=折线图, bar=柱状图
      smooth: true  // 平滑曲线
    }]
  }
  
  myChart.setOption(option)
})
</script>
```

### 6.2 柱状图与折线图的动态渲染

实际开发中，数据是从后端拿的。

```javascript
const initChart = async () => {
  const myChart = echarts.init(chartRef.value)
  myChart.showLoading() // 显示加载动画
  
  // 模拟请求
  const res = await api.getData()
  
  myChart.hideLoading() // 隐藏加载动画
  myChart.setOption({
    series: [{ data: res.data }]
  })
}
```

### 6.3 响应式图表：随窗口大小自动缩放

**问题**：当浏览器窗口变窄时，图表会被压扁或者超出屏幕。
**解决**：监听 `resize` 事件，调用 ECharts 的 `resize()` 方法。

```javascript
// 监听窗口大小变化
window.addEventListener('resize', () => {
  myChart && myChart.resize()
})

// 记得销毁监听，防止内存泄漏
onUnmounted(() => {
  window.removeEventListener('resize', ...)
})
```

---

## 第七章：个人中心与数据持久化

### 7.1 头像上传原理：Base64 vs Blob URL

前端处理图片上传有两种主流方案：

| 方案 | 原理 | 优点 | 缺点 |
| :--- | :--- | :--- | :--- |
| **Blob URL** | `URL.createObjectURL(file)` | 生成速度快 | **刷新页面失效** (内存被清空) |
| **Base64** | `FileReader` | **可持久化存储** (是字符串) | 大文件会卡顿 |

**因为我们需要把头像存在 `localStorage` 里，所以必须选择 Base64 方案。**

**代码实现：**

```javascript
const handleUpload = (file) => {
  // 1. 创建文件读取器
  const reader = new FileReader()
  
  // 2. 开始读取文件 (读成 DataURL 就是 Base64)
  reader.readAsDataURL(file.raw)
  
  // 3. 读取成功后的回调
  reader.onload = (e) => {
    // e.target.result 就是那串长长的 Base64 字符串
    const base64Str = e.target.result
    
    // 4. 更新页面显示
    userInfo.value.avatar = base64Str
    
    // 5. 存入本地缓存 (持久化)
    localStorage.setItem('userProfile', JSON.stringify(userInfo.value))
  }
}
```

### 7.2 解决“串号”问题：用户数据的隔离策略

**Bug 复现**：
1.  用户 A 登录，上传了头像，保存。
2.  用户 A 退出。
3.  用户 B 登录，竟然看到了用户 A 的头像！

**原因分析**：
`localStorage` 是浏览器公用的。如果你存数据的 key 叫 `userProfile`，那所有人登录都读这个 key，当然会串号。

**解决方案**：
在读取缓存时，加一层**身份校验**。

```javascript
onMounted(() => {
  // 1. 获取当前登录的是谁 (从 Session 或登录信息里拿)
  const currentLoginUser = JSON.parse(localStorage.getItem('userInfo'))
  
  // 2. 获取缓存的个人资料
  const savedProfile = JSON.parse(localStorage.getItem('userProfile'))
  
  // 3. 关键校验！
  // 只有当“缓存里的用户名”等于“当前登录的用户名”时，才加载缓存
  if (savedProfile && savedProfile.username === currentLoginUser.username) {
    userInfo.value = savedProfile
  } else {
    // 否则，加载默认初始数据 (防止 B 看到 A 的数据)
    userInfo.value = { 
      username: currentLoginUser.username,
      avatar: defaultAvatar 
    }
  }
})
```

### 7.3 密码修改与二次验证逻辑

修改密码是一个敏感操作，必须校验旧密码。

```javascript
const handleChangePwd = () => {
  // 1. 校验旧密码是否正确
  if (form.oldPwd !== currentUser.password) {
    return ElMessage.error('旧密码错误')
  }
  
  // 2. 校验两次新密码是否一致
  if (form.newPwd !== form.confirmPwd) {
    return ElMessage.error('两次输入的新密码不一致')
  }
  
  // 3. 更新密码
  currentUser.password = form.newPwd
  localStorage.setItem('userInfo', JSON.stringify(currentUser))
  
  // 4. 强制退出，重新登录
  ElMessage.success('修改成功，请重新登录')
  router.push('/login')
}
```

---

## 第八章：项目优化、打包与常见问题

### 8.1 代码规范：ESLint + Prettier

保持代码风格一致非常重要。建议在 VS Code 中安装 `ESLint` 和 `Prettier` 插件，并开启 "Format On Save"。

### 8.2 性能优化：路由懒加载与组件异步加载

默认情况下，打包会将所有页面打进一个巨大的 JS 文件。路由懒加载可以把不同页面拆分成不同文件，按需加载。

```javascript
// 推荐写法
{
  path: '/login',
  component: () => import('../views/Login.vue') // 只有访问 /login 时才加载这个组件
}

// 不推荐写法 (会增加首屏加载时间)
// import Login from '../views/Login.vue'
// component: Login
```

### 8.3 Vite 打包配置与生产环境部署

修改 `vite.config.js`，配置路径别名 `@`：

```javascript
import path from 'path'

export default defineConfig({
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src')
    }
  },
  // 打包去掉 console.log
  build: {
    minify: 'terser',
    terserOptions: {
      compress: {
        drop_console: true,
        drop_debugger: true
      }
    }
  }
})
```

**打包命令**：
```bash
npm run build
```
执行后会生成 `dist` 目录。把这个目录扔给 Nginx 或者 Apache 即可。

### 8.4 常见报错 (404, CORS) 及其解决方案

1.  **404 Not Found (刷新后白屏)**
    *   **原因**：单页应用 (SPA) 只有一个 `index.html`。刷新时浏览器向服务器请求 `/login`，服务器找不到这个文件。
    *   **解决**：在 Nginx 配置 `try_files $uri $uri/ /index.html;`，把所有请求都重定向回 index.html。

2.  **Element Plus 图标不显示**
    *   **原因**：没有全局注册图标。
    *   **解决**：参考第一章 `main.js` 的循环注册代码。

3.  **Setup 语法糖中无法使用 `this`**
    *   **原因**：`setup` 在 `beforeCreate` 之前执行，此时组件实例还没创建。
    *   **解决**：使用 `ref` 和 `reactive` 代替 `this`，使用 `useRouter` 代替 `this.$router`。

4.  **跨域问题 (CORS)**
    *   **现象**：控制台报错 `Access-Control-Allow-Origin`。
    *   **解决**：在 `vite.config.js` 配置代理。
    ```javascript
    server: {
      proxy: {
        '/api': {
          target: 'http://backend.com',
          changeOrigin: true
        }
      }
    }
    ```

---

## 附录：Vue3 面试高频考点

1.  **Vue2 和 Vue3 的主要区别？**
    *   响应式原理不同 (Object.defineProperty vs Proxy)。
    *   API 风格不同 (Options vs Composition)。
    *   TypeScript 支持更好。
    *   性能提升 (虚拟 DOM 算法优化)。

2.  **v-if 和 v-show 的区别？**
    *   `v-if`：真正的条件渲染，不满足条件时 DOM 元素不存在。
    *   `v-show`：通过 CSS `display: none` 切换，元素始终存在。

3.  **watch 和 computed 的区别？**
    *   `computed`：有缓存，依赖变化才重新计算，适合计算新值。
    *   `watch`：无缓存，适合监听数据变化后执行异步操作 (如发请求)。

4.  **组件通信方式有哪些？**
    *   props / emit
    *   provide / inject
    *   Pinia / Vuex
    *   attrs / slots

5.  **nextTick 是干嘛的？**
    *   等待 DOM 更新完成后执行回调。适合在修改数据后立即获取更新后的 DOM 元素。

---

> 🎉 **结语**
>
> 编程是一门实践的艺术。看完文档只是第一步，**动手把代码敲一遍**才是学会的关键。
> 遇到报错不要慌，复制报错信息去 Google 或者问 AI，解决问题的过程就是成长的过程。
>
> 祝你在前端开发的道路上，乘风破浪，Offer 多多！🚀
