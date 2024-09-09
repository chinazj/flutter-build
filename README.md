# flutter 的构建镜像
目前支持deb的版本构建。使用flutter_distributor

参考：https://medium.com/@fluttergems/packaging-and-distributing-flutter-desktop-apps-the-missing-guide-part-3-linux-24ef8d30a5b4

# 构建
直接使用下面命令构建deb

```
## 如果是amd使用下面的命令
docker run -it --rm -v <your repo>:/root/<your repo name> registry.cn-hangzhou.aliyuncs.com/tekton/linux-flutter-build:ubuntu-20.04-amd64 bash
## 如果是arm使用下面的命令
docker run -it --rm -v <your repo>:/root/<your repo name> registry.cn-hangzhou.aliyuncs.com/tekton/linux-flutter-build:ubuntu-20.04-arm64 bash
$ cd /root/<your repo name>
$ flutter pub get
$ flutter_distributor package --platform linux --targets deb
```
在最后会显示`dist/<version>/<deb>`

直接使用下面命令构建rpm
1. 修改linux/packaging/rpm/make_config.yaml，build_arch为需要编译的架构（x86_64或者aarch64）
```
vim linux/packaging/rpm/make_config.yaml
build_arch: x86_64
```

```
## amd环境
docker run -it --rm -v <your repo>:/root/<your repo name> registry.cn-hangzhou.aliyuncs.com/tekton/linux-flutter-build:fedora-38-amd64 bash
## arm环境
docker run -it --rm -v <your repo>:/root/<your repo name> registry.cn-hangzhou.aliyuncs.com/tekton/linux-flutter-build:fedora-38-arm64 bash
$ cd /root/<your repo name>
$ flutter pub get
$ flutter_distributor package --platform linux --targets rpm
```
在最后会显示`dist/<version>/<rpm>`
