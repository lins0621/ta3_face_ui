# ta+3 404-ui.

> vue 组件项目

### 快速启动

```
# 下载依赖
npm install

# 快速启动 localhost:8080
npm run dev

# 打包(完整)
npm run build

# 打包（分模块）
npm run build:modules
```

### 快速打包&发布

```
## beta 测试版
npm run publish:prerelease
## 正式发布版本
npm run publish:patch
```
#### 发布时执行的脚本分别是什么?他们代表了什么?

```
 // 拉取最新代码
 npm run git:pull
 // 更新package.json的版本号.
 // 注意: 这一步会获取git状态,如果有未提交的代码则会在此步停止发布流程
 // prerelease是获取预发布(beta)版本的版本号,即1.5.124-x;patch是获取的patch版本的版本号,即1.5.x
 npm version prerelease --unsafe-perm # npm version patch --unsafe-perm
 // 构造需要发布的包的文件,即es/lib/dist目录及web-types包,以及构造change-log
 npm run build:publish 
 // 将web-types修改提交到git仓库
 npm run git:web-types 
 // 将目前的所有未push的git记录push到远程仓库
 npm run git:push 
 // 执行clean-pkg脚本
 // 复制package.json并移除package.json中的部分内容(这部分会影响使用)
 node ./build/clean-pkg.js 
 // 执行publish,--tag表明这是一个beta版本,发布patch版本时不会传入这个tag
 npm publish --tag beta 
 // 执行restore-pkg脚本
 // 移除并恢复package.json
 node ./build/restore-pkg.js 
 // 发布lc可用的全量包
 npm run publish:lc-dist
```

### 文档
```
# 打包（分模块）
npm run build:modules

# 开发模式API文档
npm run site:dev

# 打包API文档
npm run site:build

# WebStorm/IDEA 使用的webtypes
npm run build:webtypes

```

### 主题
```
# dev模式下在线切换皮肤 
npm run dev:theme

# 编译出默认主题色的打包
npm run build:theme

```
