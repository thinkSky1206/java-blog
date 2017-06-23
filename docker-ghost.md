#1 安装docker和ghost镜像
ssh root@ip  


yes

sudo yum install docker

sudo service docker start 启动docker

sudo chkconfig docker on  设置开机启动

docker pull ghost

docker run --name blog -p 8080:2368 -d ghost

通过ip访问 ip:8080

#2 绑定域名
yum  install nginx

vi /etc/nginx/conf.d/ghost.conf 添加配置

server {  
listen 80;  
server_name liuwuping.me;

location / {  
    proxy_set_header   X-Real-IP $remote_addr;
    proxy_set_header   Host      $http_host;
    proxy_pass         http://127.0.0.1:8080;
}
}

service nginx restart 重启nginx

>参考资料
>
>[使用 Docker 部署 Ghost 教程](https://sspai.com/post/36751)

