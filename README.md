# flutter 的构建镜像
目前支持deb的版本构建。使用flutter_distributor

参考：https://medium.com/@fluttergems/packaging-and-distributing-flutter-desktop-apps-the-missing-guide-part-3-linux-24ef8d30a5b4

# 构建
直接使用下面命令构建deb

```
docker run -it --rm -v <your repo>:/root/<your repo name> <image-name>:<image-tag> bash
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
docker run -it --rm -v <your repo>:/root/<your repo name> <image-name>:<image-tag> bash
$ cd /root/<your repo name>
$ flutter pub get
$ flutter_distributor package --platform linux --targets rpm
```
在最后会显示`dist/<version>/<rpm>`
