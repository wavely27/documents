# 常问原理与流程问题

## webpack

### webpack 优化方案

- 寻址优化
  优化 loader 解析范围
  优化模块查找路径[modules \ mainFields \ alias \ extensions]
  忽略外部模块解析 (module.noParse)
- 优化打包效率
  启用多进程 (TerserWebpackPlugin \ HappyPack \ ParallelUglifyPlugin)
  使用编译缓存 (webpack5[cache:{ type:"filesystem”}] \ hardSourcePlugin \ DllPlugin \ loader?cacheDirectory)
- 开发体验优化
  自动刷新
  HMR
- 打包结果优化
  区分环境 （删除不必要的 loader plugin \ 区分 devTool）
  提取公共代码 (commonChunk)
  压缩代码 (TerserWebpackPlugin \ optimize-css-assets-webpack-plugin \
   hteml-webpack-plguin minify)
  优化图片 (url-loader limit \ 压缩图片 image-webpack-loader \ )
  启用 Tree Shaking
  启用 prepack (部分自动求值器)
  启用 ScopeHoisting (作用域合并)
- 项目加载优化
  CDN 加速 (使用 externals 引入公共 CDN)
  使用长久缓存 (强缓存 \ recordsPath \ hash \ [分离\内联]runtime \ 稳定 moduleId)
  代码拆分 (按需加载 \ Mini-css-extract-plugin)
  使用按需加载 \ 懒加载 \ 预加载 (import(/_ webpackPrefetch: true _/ 'lodash'))
  browserslist
- 编译分析
  speed-measure-webpack-plugin (快速测量各插件和 loader 的耗时)
  profilingPlugin (创建构建性能报告)
  webpack-bundle-analyzer (内容体积分析[stat\parsed\gzip])
  配置 profile (生成详细打包报告)

### webpack 流程

- 1.初始化配置
- 2.初始化 compiler 对象 加载 plugin（监听事件广播）
- 3.通过 entry 分析目录
- 4.开始逐个模块编译 通过 loader 进行代码转换
- 5.梳理所有模块依赖 生成 chunk
- 6.输出结果文件

### Tabable 原理

### 常用 loader

url-loader css-loader style-loader babel-loader

### 常用 plugin

html-webpack-plugin terser-webpack-plugin mini-css-extract-plugin webpack.DefinePlugin

### plugin 实现原理

- 1.配置读取过程 初始化 Plugin 实例
- 2.初始化 compiler 对象后 调用 Plugin.apply 传如 compiler 对象
- 3.通过 compiler.plugin 事件广播

## react

### virtual dom 原理

vdom 是用来映射真实 dom 的简单 JS 对象，操作不会有副作用。所以用 vdom 结合 diff 算法 然后通过批量操作真实 dom 来优化渲染。减少浏览器重拍重绘优化性能。

### diff 算法

三大策略来优化 diff:

- tree diff (两棵树只会对同一层次的节点进行比较，忽略 DOM 节点跨层级的移动操作 [保持 DOM 结构稳定])
- component diff (同类型组件 继续比较 vdom 不同类型直接替换 [用 shouldComponentsUpdate 来优化避免继续比较])
- element diff (对同层级的一组节点用 key 优化: 插入、移动、删除 [ 避免后元素前移])

### diff 算法的异同

#### 相同点:

- 都不做跨层级比较

#### 不同点:

- 1.Vue 一边 diff 一边 patch
- 2.元素类型相同 className 不同 Vue 会重新创建 React 会修改
- 3.列表比较 Vue 用双指针 React 用单指针

### setState 流程与原理

setState 是 react 推荐的状态更新方式 分为同步异步两种
在生命周期与合成事件中 react 的表现是异步的。在原生时间和定时器等事件循环中 表现为同步
同步情况下 调用 setState 之后 立即执行状态更新
异步情况下 调佣 setState 之后 会将更新操作进行合并 实现批量状态更新
状态更新前会触发 componentWillReceiveProps getDerivedStateFromProps 以及 shouldComponentUpdate
状态更新后会触发 getSnapshotBeforeUpdate
然后执行 render 方法 通过虚拟 DOM 树和 diff 算法 增量更新视图
老流程 通过队列完成合并更新 然后通过遍历 dirtyComponent 并执行 updateComponent 完成更新
新流程 通过 update 对象 更新 fiber 树 执行调度方法 然后进入 render 阶段 和 commit 阶段 完成更新
完成之后会触发 DidMount 和 DidUpdate

### hooks 实现原理

react 组件用链表链表维护了一个 Hooks 列表
列表体现了每个 hook 的顺序 并记录了每个 hook 的状态或依赖
fiberNode.memoizedState 指向 Hook (memoizedState 保存状态 queue 批量保存更新操作)
fiberNode.updateQueue 指向 Effect (组件完成渲染后遍历链表执行 deps 保存依赖的状态 tag 标记变化 \ 先清除上一轮的副作用 然后再执行本轮的 effect 的)

### fiber 实现原理

## redux

三大原则: 单一数据源 \ state 只读 \ reducer 是纯函数

### redux 原理

通过 createStore 创建 store 对象
通过 第一个参数 传入 reducer 初始化 state 更新操作
通过 store.subscribe 方法 实现订阅 绑定 state 更新的回调
通过 store.dispatch 方法 传入 action 对象 实现发布 触发 state 更新

## mobx

### mobx 原理

## 微前端

### 什么是独立运行时 如何实现
