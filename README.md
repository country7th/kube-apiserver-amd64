解决gcr.io/google_containers/kube-apiserver-amd64:v1.7.3镜像下载失败的解决方案
2019年04月18日

      可能由于某些原因，导致gcr.io/google_container的镜像无法下载，经过测试，可能通过普通的翻墙也会下载失败。
      目前一个常见的解决方案是使用Docker Hub来做一个代理。步骤如下：
编写Dockerfile，然后提交到Github。Dockerfile只需用一行代码：
也就是你要真正拉取的镜像名称，把该镜像作为一个基础镜像即可。
FROM gcr.io/google_containers/kube-apiserver-amd64:v1.7.3

目前该Dockerfile的Github仓库地址为：https://github.com/country7th/kube-apiserver-amd64

使用Docker Hub的Automated Build来进行构建，把自动构建的仓库设置为Github的仓库地址即可。

选择自动构建

然后在右侧选择你在Github中gcr仓库地址即可：

然后Docker Hub就会帮你自动构建了：


目前该镜像的仓库地址为：https://cloud.docker.com/repository/docker/country7th/kube-apiserver-amd64/
可以直接通过以下命令拉取：
docker pull country7th/kube-apiserver-amd64


通过以上命令拉取的镜像其实就是一开始被墙的“gcr.io/google_containers/example-guestbook-php-redis:v3”镜像。其他的镜像也可以通过该种方式替代。