---
title: 关于Docker的使用
tags: Docker
categories: Docker
abbrlink: ad37
date: 2023-12-26 22:00:00
updated: 2023-12-26 22:30:00
cover: 
---

# 简介
- Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux
# docker
- 制作镜像
    - 在要制作镜像的项目根目录编写 `Docckerfile`： 
```bash
# 通过FROM关键词，例如我需要一个python3.6的环境：

FROM python:3.6

# 我们只需要在Dockerfile里面编写如上的代码，就能够拉取到一个python3.6的环境。
# 同理其他语言也是，例如.net：

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base

# 还有前端项目：

FROM nginx

# 具体的环境大家可以通过docker search 来进行搜索。
# 这是我们的第一步。
# 下一步我们也许会去定一个根目录，注意是也许，不是一定。

WORKDIR /app

# WORKDIR的意思就是让后面的路径成为根路径，注意哦，这里的路径是docker里面的路径。
# 然后，我们就会把代码或者是编译完成之后的运行文件COPY到docker当中

COPY . .

# 上面就是COPY+本地路径 +docker中的路径
# 也就是本机当前路径文件，拷贝到docker中的路径中。
# 在Python中，我们还需要去安装一些Python库，所以你可能还需要这个操作：

RUN pip install -r requirements.txt

# RUN 后面接的就是一个命令行。

# 安装完成之后，你需要去暴露一下端口

EXPOSE 80

# 这样能够让我们后续将docker中的端口和本机中的端口进行映射，从而我们可以通过本机ip+端口来进行访问操作。
# 最后一步就是运行，当然如果是Python我们就可以直接运行了，但是有一些语言框架可能不行，因为它可能还需要进行一次编译，然后再运行编译后的文件，所以这里大家需要注意了。
# 如果你不想在docker打包过程中编译，你也可以在本机中编译完，直接运行编译后的文件。
# 当然在Python中我们直接运行Python即可。

CMD ["python","main.py"]

# 在.NET环境下可能就是这样的姿势：

ENTRYPOINT ["dotnet", "HubService.dll"]

# 在前端项目中，我们就不需要再去运行啥，直接部署到Nginx上就行了，例如下面：

FROM nginx
COPY dist/ /usr/share/nginx/html/
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# 也就是我们自己在本机上写个Nginx的配置文件，然后COPY过去就行了。
# 好了，上面大致就是打包的整个过程与思路，每个框架，每个语言都会有不一样，所以没有准确的答案，准确的答案在官方文档中一般有所体现。
# 这里也给大家汇总一下python的dockerfile

FROM python:3.6
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 80
CMD ["python","app.py"]

# 打包QPDBot的代码
FROM python:3.10
WORKDIR /app
COPY . /app
VOLUME /app/config

RUN pip config set global.index-url http://mirrors.aliyun.com/pypi/simple
RUN pip config set install.trusted-host mirrors.aliyun.com
RUN pip install -U pip

RUN pip install -r requirements.txt
CMD ["python","main.py"]

# 编写完dockerfile，我们一般喜欢放在需要打包的地方的根路径，然后直接运行

docker build -t 你想要的名字 . 

# 运行之后，docker会自动完成dockerfile里面的每一个步骤。
# 打包完成后，我们就可以看到images。
# 大家直接docker images 即可。
# 随后，我们就可以来创建容器了。

docker run --name=QPDBot -d -v /path/to/config:/app/config rjxinsi/qpdbot:latest

```
- 发布镜像
```shell
# 如果没有登录，先登录
docker login

# 使用如下的指令就给本地镜像打tag

docker tag myImage:v1 your_user_name/myImage:v1

# 之后push

docker push your_user_name/myImage:v1

```