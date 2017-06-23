#docker-componse


	curl -L https://get.daocloud.io/docker/compose/releases/download/1.14.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
	
	chmod +x /usr/local/bin/docker-compose
	
#harbor

	cd /home/lwp
	
	#下载
	wget https://github.com/vmware/harbor/releases/download/v1.1.2/harbor-offline-installer-v1.1.2.tgz
	
	#解压
	tar xvf harbor-offline-installer-<version>.tgz
	
	#配置harbor.cfg
	cd harbor
	hostname：外网可以访问的ip
	
	#配置docker 
	--insecure-registry 192.168.10.10
	重新启动damon 和docker
	
	
	#安装
	./install.sh
	