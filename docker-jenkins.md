#创建host数据文件夹
mkdir /home/lwp/jenkins

chown 1000:1000 /home/lwp/jenkins

docker run -p 8080:8080 -p 50000:50000 -v /home/lwp/jenkins:/var/jenkins_home --name my_jenkins -d jenkins


#jenkins设置

###maven

系统管理-Global Tool Configuration-maven 勾选自动安装-保存

系统管理-Managed files-Add new Config-Gloal Maven Settings.xml


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