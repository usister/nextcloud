# nextcloud
A docker compose yaml for nextcloud and collabora code.
一个nextcloud的docker compose文件，使用自签名证书，独立部署mariadb和collabora code。
# 使用方法
## 克隆项目
    git clone https://github.com/usister/nextcloud.git
## 修改.env文件
根据.env文件中的注释内容，修改环境变量，必须要修改的有
1. DOMAIN_NAME=172.16.2.67.sslip.io
2. 把172.16.2.67改成自己的ip地址，或者把172.16.2.67.sslip.io改成你的域名

**注意：不建议将IP地址或域名设置为本地回环地址**
1. 因为docker的默认网络安全限制，容器无法访问主机网络，所以当设置成127.0.0.1.sslip.io时，app容器无法通过proxy容器访问collabra容器。一定要用127.0.0.1时，需要手动调整collabora到host网络，未作测试，也不建议这么做；
2. 理论上将域名设置为localhost也会遇到上面的问题，使用localhost域名未做测试，所以也不建议这么做；

推荐修改：
    --o:admin_console.username=username --o:admin_console.password=password
    修改成自己的用户名和密码
## 运行容器
    docker pull nginx:alpine
    cd nextcloud
    docker-compose up -d
## 初始化nextcloud
浏览器访问 https://your_ip_address.sslip.io 或 https://your_domain.sslip.io

![Initial_Iamge](https://raw.githubusercontent.com/usister/nextcloud/refs/heads/main/image/initial.png)

输入要设置的用户名和密码，点击安装开始初始化。安装推荐的应用：

![Install_Apps](https://github.com/usister/nextcloud/blob/main/image/install_recommend_apps.png?raw=true)

**注意**大陆地区如果未设置代理，有可能出现安装不成功。

## 设置collabora code
1. 点击右上角的用户头像，选择“管理设置”
![Setup_Code_1](https://github.com/usister/nextcloud/blob/main/image/setup_code_1.png?raw=true)
2. 在左下角找到“office”，选择“使用您的自有服务器”，输入访问nextcloud的url，点击“Save”
url为 https://your_ip_address.sslip.io 或 https://your_domain.sslip.io 不需要额外的路径。

![Setup_Code_2](https://github.com/usister/nextcloud/blob/main/image/setup_code_2.png?raw=true)

## 停止所有容器
    docker-compose down

## 清理及删除
**<font color=#FF3030>注意，这会删除用户数据，除非你确定删除，否则不要执行下面的命令。</br>建议参考docker手册管理卷</font>**

    docker-compose down -v

# 注意事项
collabora code使用nextcloud用于在线编辑的外置服务器，目前没有好的身份验证手段，因此本项目只局限在局域网使用。如果要关闭collabora code，在运行后手动停止/删除 code容器，或者运行前注释掉 compose.yaml文件中的code部分。

#