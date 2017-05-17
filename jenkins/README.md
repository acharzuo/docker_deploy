# 持续集成软件Jenkins 的docker部署

## 构建
```
 docker build -t "achar/jenkins" .
```
注意后面的点。

## 构建错误后的处理

查看当前已经构建完成的镜像，并启动镜像
```
docker images  # 查看已生成的镜像，部分生成的镜像
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              31b858bcd89d        2 hours ago         797 MB

docker run -i --name jenkins 31b858bcd89d /bin/bash  # 启动指定ImageId的容器

root@d0d82c2df589:/#    # 进入容器内部命令行
``` 
查找构建失败的原因， 重新编辑Dockerfile文件，继续构建

```
docker build --no-cache -t achar/jenkins .   # 清除已经构建的缓存重新构建
```

## 启动Jenkins容器
```
docker run -p 8080:8080 --name jenkins --privileged -d achar/jenkins
```


