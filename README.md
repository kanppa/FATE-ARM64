# FATE-ARM64

NOTE:
- 本项目只用于构建docker镜像，目前只适配v1.7.2版本，其他版本未测试
- python-client和python-nn模块没有，由于用不到，未进行测试
- 几个base-image的选择可能不是最优的
- arm64 ubuntu 和 m1 pro测试通过所有的test suite （nn除外）


使用：

> 将 build-arm 目录拷贝到FATE项目根目录下

```
cd build-arm/docker-build
bash build_cluster_docker.sh all
```
