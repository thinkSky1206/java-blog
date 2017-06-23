>参考资料
>
>[Jenkins 2 Tutorial For Beginners - Getting Started Guide]
(https://devopscube.com/jenkins-2-tutorials-getting-started-guide/)

>[Jenkins 与 Docker 的持续集成实践一](https://addops.cn/post/jenkins-docker-01.html)
>
>[Jenkins+Docker搭建持续集成测试环境](http://dockone.io/article/1464)
>
>[Execute Jenkins Maven builds in Docker containers](http://christoph-burmeister.eu/?p=2989)
>
>bug
>
>[How do i expose the Docker Remote API on Centos 7?](https://stackoverflow.com/questions/40242522/how-do-i-expose-the-docker-remote-api-on-centos-7)
>
>[Exposing Docker Remote API v1.22 on CentOS7](https://stackoverflow.com/questions/41730129/exposing-docker-remote-api-v1-22-on-centos7)

	node("master") {
	
	    stage('Configure') {
	    env.PATH = "${tool 'maven-3.5.0'}/bin:${env.PATH}"
	    }
	
	    stage('Checkout') {
	        git 'https://github.com/thinkSky1206/spring-boot-tutorial.git'
	    }
	
	    stage('Build') {
	     configFileProvider([configFile(fileId: 'cece87f9-8459-4936-ba6d-6afadc79d557', variable: 'MAVEN_SETTINGS')]) {
	      sh 'mvn -s $MAVEN_SETTINGS clean package'
	    }
	
	
	    }
	
	
	}


#创建host数据文件夹
mkdir /home/lwp/jenkins

chown 1000:1000 /home/lwp/jenkins

docker run -p 8080:8080 -p 50000:50000 -v /home/lwp/jenkins:/var/jenkins_home --name my_jenkins -d jenkins


#jenkins设置

###maven

系统管理-Global Tool Configuration-maven 勾选自动安装-保存

系统管理-Managed files-Add new Config-Gloal Maven Settings.xml


###插件

simple theme:更改样式插件

docker plugin: 将docker容器作为slave


#Pipeline

新建-pipeline

Build periodically ： 0 1 * * *   //每天凌晨1点触发

Pipeline syntax:辅助脚本编写



	node("master") {
	    
	    stage('Configure') {
	    env.PATH = "${tool 'maven-3.5.0'}/bin:${env.PATH}"
	    }
	    
	    stage('Checkout') {
	        git 'https://github.com/thinkSky1206/spring-boot-tutorial.git'
	    }
	    
	    stage('Build') {
	     configFileProvider([configFile(fileId: 'cece87f9-8459-4936-ba6d-6afadc79d557', variable: 'MAVEN_SETTINGS')]) {
	      sh 'mvn -s $MAVEN_SETTINGS clean package'
	    }
	
	    
	    }
	    
	    
	}
	
	
	
	
	