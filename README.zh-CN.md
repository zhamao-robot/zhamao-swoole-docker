# zhamao-swoole-docker 中国版

主要是提供 zhamao 的开发环境，与其他 `Swoole` 项目兼容，开发 `Swoole` 相关程序必备！


## 要求

安装了 `Docker` 和 `docker-compose`。 `Windows` 和 `Mac` 自带 `docker-compose` 命令。`Linux` 用户需自行安装。

- [Docker 安装](https://docs.docker.com/get-docker/)
- [docker-compose 安装](https://docs.docker.com/compose/install/)


## 配置

1. 设置 `docker-compose.cn.yml` 中的项目目录映射
2. 下载 `Swoole`、`redis` 扩展包，推荐使用以下两个版本（不同版本的依赖可能会有变化）
    - [redis-5.3.5RC1.tgz](http://pecl.php.net/get/redis-5.3.5RC1.tgz)
    - [swoole-4.8.2.tgz](http://pecl.php.net/get/swoole-4.8.2.tgz)
3. 放置到 `pecl` 目录中

> Note:
>
> 我知道有 `pecl install` 命令，会出现请求失败，所以干脆自行下载包，后面换版本还可以复用。 


## 使用方法

初始化环境，修改了 `docker-compose.cn.yml` 使用以下命令也可以重新初始化。

```shell
docker-compose up -f docker-compose.cn.yml -d
```

> Note:
>
> 修改 `docker-compose.cn.yml` 为 `docker-compose.yml` 可以省略 `-f docker-compose.cn.yml` 参数


`Dockerfile.cn` 文件修改了则需要使用以下命令更新镜像。

```shell
docker-compose build -f docker-compose.cn.yml
```


日常使用

```shell
docker-compose start
docker-compose restart
docker-compose stop
```

### 开发常用命令

进入容器

```shell
docker exec -it zhamao-php74 /bin/sh
# 或
docker exec -it zhamao-php74 sh 
```

安装项目依赖

```shell
composer install
```

启动项目

```shell
vendor/bin/start server
```

> Note:
>
> 默认进入 `Dockerfile.cn` 设置的 `/app` 工作目录，如果修改了需要自行切换。


## 小技巧

### 修改 Dockerfile 时实例一个容器进入操作，操作成功才记录修改

可以得到容器的实时反馈，及时补充依赖和修改错误。

### docker-php-ext-install 尽可能的一次性执行完需要安装的扩展

如果仔细查看命令返回信息，会发现自主安装清除编译依赖，所以能一次性执行完会省一次资源。
