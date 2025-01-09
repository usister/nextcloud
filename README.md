# nextcloud
A docker compose yaml for nextcloud and collabora code.
一个nextcloud的docker compose文件，使用自签名证书，独立部署mariadb和collabora code。
# 使用方法
## 克隆项目
    git clone https://github.com/usister/nextcloud.git
## 修改.env文件
根据.env文件中的注释内容，修改环境变量，必须要修改的有
    DOMAIN_NAME=127.0.0.1.sslip.io
    把localhost改成自己的ip地址或域名
推荐修改：
    --o:admin_console.username=username --o:admin_console.password=password
    修改成自己的用户名和密码

## 运行容器
    docker pull nginx:alpine
    cd nextcloud
    docker-compose up -d
## 配置collabora code
    浏览器访问 https://your_ip_address.sslip.io 
![Initial_Iamge](https://raw.githubusercontent.com/usister/nextcloud/refs/heads/main/image/initial.png)
## 停止容器
    docker compose down
## 清理及删除
参考docker手册
# 注意事项
collabora code使用nextcloud用于在线编辑的外置服务器，目前没有好的身份验证手段，因此本项目只局限在局域网使用。如果要关闭collabora code，在运行后手动停止/删除 code容器，或者运行前注释掉 compose.yaml文件中的code部分。