## [npm太慢， 淘宝npm镜像使用方法](https://blog.csdn.net/quuqu/article/details/64121812)

### 1.临时使用

```
npm --registry https://registry.npm.taobao.org install express
```

### 2.持久使用

```
npm config set registry https://registry.npm.taobao.org
```

### 3.通过cnpm使用

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```



## 包管理

1、全局安装 npm install -g npm-check

2、npm-check -u -g

3、通过上下键可以移动光标，使用空格键可以选择需要处理的包，回车直接进行处理。