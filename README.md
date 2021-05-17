# 应用分发平台 (暂时还没想好起什么名字)

## 背景
> 之前公司一直在使用某分发平台托管生产 App, 直到有一天公司的帐号被平台封禁封禁, 导致所有 App 都不能下载了. 在此情形之下, 我决定写一个自用的应用分发平台. 自此之后, 这个项目就建立了.

## 简介
有一些时候, 我们并不需要将 App 上架应用商店, 但是我们又希望能维护 App 版本, 这个时候就需要用到分发平台. 但是很多分发平台不是收费, 就是乱七八糟的各种条款, 让生产使用变得困难. 如果用户能自己维护分发平台, 那么就不需要再去找七七八八的其他平台了.

## 功能
1. 管理 Android 和 Apple 的 App 包信息.
2. 维护 App 包的更新记录.
3. 提供 App 分享页面, 供客户下载使用.
4. 提供更新 api, 客户端自行对接后可实现应用自更新.

## 运行
因为后端是用 golang 实现, 编译时依赖 gcc, 但每个平台的 gcc 版本不同, 无法保证一次编译, 到处运行. 所以需要用户自己编译后运行. 当然配置好 golang 环境直接运行也是可以的.

### 开发环境运行

#### 要求

* git
* npm > 7 or yarn > 1.22
* golang > 1.16

1. 拉取代码到本地
```
git clone https://github.com/AkariMarisa/app-management-platform
cd app-management-platform
```
2. 运行后端
```
cd app-management-platform-back-end
go get
go run main.go
```
3. 运行前端
```
cd ../app-management-platform-front-end
yarn # 如果你使用 npm 而不是 yarn 的话, 则是 npm install
yarn serve # 如果你使用 npm 而不是 yarn 的话, 则是 npm run serve
```

### 生产环境编译

#### 要求

* make > 4.3
* upx 3.96
* tar

1. 编译前端
```
cd app-management-platform/app-management-platform-front-end
yarn build
```
2. 复制前端文件到后端目录
```
cp -r dist/* ../app-management-platform-back-end/public
```
3. 编译后端
```
cd ../app-management-platform-back-end
make build
```
4. 压缩后端(可选)
```
make compress
```
5. 打包后端
```
make package
```

打包后的文件位于 app-management-platform/app-management-platform-back-end/out/ 目录下,
其中 dist_linux.tgz 为 linux 版本, dist_win.tgz 为 windows 版本.

拷贝需要的压缩包, 放到生产环境下解压, 执行`./main_linux`或`./main_win.exe`运行服务.

### 未来可能实现的功能

- [] 支持英文.
- [] 按应用限制下载次数(每天, 每周, 每月).
- [] 应用下载记录图表.
- [] 用户可以设置应用的上线商店地址, 客户打开分享页时直接跳往商店.
- [] 生成应用版本差分包, 减少每次客户端更新的下载大小.

### 提交 issue

技术问题或 bug 提交, 请到[前端](https://github.com/AkariMarisa/app-management-platform-front-end)或[后端](https://github.com/AkariMarisa/app-management-platform-back-end)的仓库单独提交, 其他问题请提交到此仓库.