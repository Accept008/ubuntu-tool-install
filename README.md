# ubuntu-tool-install

### 0.1 QQ安装
        https://im.qq.com/linuxqq/download.html（下载x64版本）
		wget https://qd.myapp.com/myapp/qqteam/linuxQQ/linuxqq_2.0.0-b1-1024_amd64.deb
        双击就能安装（linuxqq_2.0.0-b1-1024_amd64.deb）
### 0.2 openvpn安装（公司数据库需要vpn才能访问数据库）
	https://www.bbsmax.com/A/QV5Z9NGwJy/
	root@chen:/home/chen# sudo apt-get install openvpn
	
	chen@chen:~/Downloads/qq-files/1550581389/file_recv/openvpn_aws_5/openvpn_aws$ su root
	密码： 
	root@chen:/home/chen/Downloads/qq-files/1550581389/file_recv/openvpn_aws_5/openvpn_aws# cp 222_client.ovpn /etc/openvpn
	root@chen:/home/chen/Downloads/qq-files/1550581389/file_recv/openvpn_aws_5/openvpn_aws# ls
	222_client.ovpn  ca.crt  shane.crt  shane.key
	root@chen:/home/chen/Downloads/qq-files/1550581389/file_recv/openvpn_aws_5/openvpn_aws# cp ca.crt /etc/openvpn
	root@chen:/home/chen/Downloads/qq-files/1550581389/file_recv/openvpn_aws_5/openvpn_aws# cp shane.crt /etc/openvpn
	root@chen:/home/chen/Downloads/qq-files/1550581389/file_recv/openvpn_aws_5/openvpn_aws# cp shane.key /etc/openvpn
	root@chen:/home/chen/Downloads/qq-files/1550581389/file_recv/openvpn_aws_5/openvpn_aws# 
	
	
	将服务端提供的文件放在此文件夹下 /etc/openvpn/
	a启动b
		root@chen:/etc/openvpn# ls
		222_client.ovpn  client  server  update-resolv-conf
		root@chen:/etc/openvpn# ls
		222_client.ovpn  client  shane.crt  update-resolv-conf
		ca.crt           server  shane.key
		root@chen:/etc/openvpn# openvpn 222_client.ovpn

		
		root@chen:/etc/openvpn# cd /etc/openvpn/
		root@chen:/etc/openvpn# openvpn 222_client.ovpn
		Ctrl + C停止
	
## 1.设置初始root密码
    sudo passwd root

## 2.安装vim工具
    sudo apt install vim
    
## 3.创建工具安装文件夹
    chen@chen:/usr/local$ sudo mkdir tool
    chen@chen:~$ su root
    密码： 
    root@chen:/home/chen# sudo mkdir package

## 4.Java离线安装
### 复制安装包
    root@chen:/home/chen# cd package （jdk-8u231-linux-x64.tar.gz在package文件夹）
    root@chen:/home/chen/package# sudo cp jdk-8u231-linux-x64.tar.gz /usr/local/tool/(复制)
### 解压配置环境变量
    chen@chen:/usr/local/tool$ sudo tar -vxf jdk-8u231-linux-x64.tar.gz
    root@chen:/usr/local/tool# rm -rf jdk-8u231-linux-x64.tar.gz（移除安装包）
    sudo vim /etc/profile
      将信息加在profile文件最后面：
		  export JAVA_HOME=/usr/local/tool/jdk1.8.0_231
		  export JRE_HOME=$JAVA_HOME/jre
		  export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib/rt.jar
		  export PATH=$PATH:$JAVA_HOME/bin
    保存profile，不重启生效命令: root@chen:sudo source /etc/profile（目前不生效，直接选择重启）
    java -version （查看安装信息）
    
  ## 5.maven安装
  ### 安装包处理
  	root@chen:/home/chen/package# sudo cp apache-maven-3.5.2-bin.tar.gz /usr/local/tool（复制）
	root@chen:/usr/local/tool# sudo tar -zxvf apache-maven-3.5.2-bin.tar.gz（解压）
	sudo rm -rf apache-maven-3.5.2-bin.tar.gz（移除安装包）
  ### settings.xml文件更换
  	root@chen:/usr/local/tool# sudo mkdir maven-repo（创建本地依赖库）
	root@chen:/usr/local/tool# sudo chmod -R 777 /usr/local/tool/maven-repo（设为都有权限）
	root@chen:/usr/local/tool# sudo chmod -R 777 /usr/local/tool/apache-maven-3.5.2/conf/
	可视化移动settings.xml和jar包依赖
  ### 配置环境变量：
	sudo vim /etc/profile
	加在最后：
		export M2_HOME=/usr/local/tool/apache-maven-3.5.2i
		export CLASSPATH=$CLASSPATH:$M2_HOME/lib
		export PATH=$PATH:$M2_HOME/bin
		
	重启生效（或执行 source /etc/profile）
## 6.git安装
	root@chen:/home/chen# sudo apt-get update
	sudo apt install git
	git --version
	git config --global user.name "chenjiacheng"
	git config --global user.email "chenjiacheng@soundbus.cn"
	git config --list
## 7.idea安装
	http://www.jetbrains.com/idea/
	http://www.jetbrains.com/idea/download/other.html
	wget https://download.jetbrains.8686c.com/idea/ideaIU-2018.3.6.tar.gz?_ga=2.249811142.197179249.1578351703-410511996.1578351703
### 安装包处理
	root@chen:/media/chen/LENOVO/ubuntu-package# sudo cp ideaIU-2018.3.6.tar.gz /usr/local/tool/（复制）
	root@chen:/usr/local/tool# sudo tar -vxf ideaIU-2018.3.6.tar.gz（解压）
	sudo rm -rf ideaIU-2018.3.6.tar.gz（移除安装包）
### 破解
	root@chen:/media/chen/LENOVO/ubuntu-package# sudo cp JetbrainsCrack-4.2-release-enc.jar /usr/local/tool（复制）
	sudo chmod 755 idea-IU-183.6156.11/（修改权限）
	sudo chmod 755 JetbrainsCrack-4.2-release-enc.jar（修改权限）
	下面2个文件最后一行加入破解jar： -javaagent:/usr/local/tool/JetbrainsCrack-4.2-release-enc.jar
		cd idea-IU-183.6156.11/bin/
		sudo vim idea.vmoptions
		sudo vim idea64.vmoptions
### 加入全局快捷方式
	su root 
	cd /usr/share/applications
	sudo gedit idea.desktop
    	添加以下代码
		[Desktop Entry]
		Version=2018.3.6
		Name=IntelliJ IDEA
		Exec=/usr/local/tool/idea-IU-183.6156.11/bin/idea.sh
		Icon=/usr/local/tool/idea-IU-183.6156.11/bin/idea.png
		Terminal=false
		Type=Application
		Categories=Development
	桌面左下角查看（在dash中看到xxx的启动器图标了，也可以直接将其添加锁定到launcher）
### 开启idea后,输入注册信息
	ThisCrackLicenseId-{
	“licenseId”:”ThisCrackLicenseId”,
	“licenseeName”:”idea”,
	“assigneeName”:”“,
	“assigneeEmail”:”idea@163.com”,
	“licenseRestriction”:”For This Crack, Only Test! Please support genuine!!!”,
	“checkConcurrentUse”:false,
	“products”:[
	{“code”:”II”,”paidUpTo”:”2099-12-31”},
	{“code”:”DM”,”paidUpTo”:”2099-12-31”},
	{“code”:”AC”,”paidUpTo”:”2099-12-31”},
	{“code”:”RS0”,”paidUpTo”:”2099-12-31”},
	{“code”:”WS”,”paidUpTo”:”2099-12-31”},
	{“code”:”DPN”,”paidUpTo”:”2099-12-31”},
	{“code”:”RC”,”paidUpTo”:”2099-12-31”},
	{“code”:”PS”,”paidUpTo”:”2099-12-31”},
	{“code”:”DC”,”paidUpTo”:”2099-12-31”},
	{“code”:”RM”,”paidUpTo”:”2099-12-31”},
	{“code”:”CL”,”paidUpTo”:”2099-12-31”},
	{“code”:”PC”,”paidUpTo”:”2099-12-31”} ],
	“hash”:”2911276/0”,
	“gracePeriodDays”:7,
	“autoProlongated”:false}
### maven、git配置、装插件lombok、kubernates
	git为默认安装不用配
	root@chen:/usr/local/tool# sudo chmod -R 777 /usr/local/tool/（软件包权限都开启）
### 导入readme项目
	先建个demo项目配置下JDK
	https://github.com/Accept008/readme.git
### 切换到root后环境变量无效（不能使用java -version）

	在/root/.bashrc文件后面加入: source /etc/profile
    	sudo vim /root/.bashrc
    	加入：source /etc/profile
    	重启

## 8.postman安装
	https://www.getpostman.com/downloads/
	chen@chen:~/下载$ su root
	密码： 
	root@chen:/home/chen/下载# cp Postman-linux-x64-7.14.0.tar.gz /usr/local/tool/
	root@chen:/home/chen/下载# cd /usr/local/tool/
	root@chen:/usr/local/tool# ls
	apache-maven-3.5.2      JetbrainsCrack-4.2-release-enc.jar
	electron-ssr-0.2.5.deb  maven-repo
	idea-IU-183.6156.11     node-v12.14.0-linux-x64
	jdk1.8.0_231            Postman-linux-x64-7.14.0.tar.gz
	root@chen:/usr/local/tool# sudo tar -xzf Postman-linux-x64-7.14.0.tar.gz
	### 加入全局快捷方式
	su root 
	cd /usr/share/applications
	sudo gedit postman.desktop
    	添加以下代码
	[Desktop Entry]
		Encoding=UTF-8
		Name=Postman
		Exec=/usr/local/tool/Postman/Postman
		Icon=/usr/local/tool/Postman/app/resources/app/assets/icon.png
		Terminal=false
		Type=Application
		Categories=Development;
##  9.robot3T安装
	下载：https://robomongo.org/download
	a.下载安装
	su root
	sudo cp robo3t-1.3.1-linux-x86_64-7419c406.tar.gz /usr/local/tool/
	cd /usr/local/tool/
	sudo tar -zxvf robo3t-1.3.1-linux-x86_64-7419c406.tar.gz

	在robot bin目录下载图标
	    wget https://robomongo.org/static/robomongo-128x128-129df2f1.png

	b.配置启动方式
	su root
	cd /usr/share/applications
	sudo gedit robo3t.desktop
	添加以下代码
	    [Desktop Entry]
	    Version=1.3.1
	    Name=Robo3T
	    Exec=/usr/local/tool/robo3t-1.3.1-linux-x86_64-7419c406/bin/robo3t
	    Terminal=false
	    Icon=/usr/local/tool/robo3t-1.3.1-linux-x86_64-7419c406/bin/robomongo-128x128-129df2f1.png
	    Type=Application
	    Categories=Development
	ll 命令查看
	桌面左下角查看（在dash中看到xxx的启动器图标了，也可以直接将其添加锁定到launcher）
	
## 10.redis可视化工具安装
    显示应用程序 -> Ubuntu软件 -> 搜索【P3X Redis UI】点击安装

![image](./redis-view.png)   
    	
## 11.mysql可视化安装
    a.workbench
        sudo apt-get install mysql-workbench
    b.navicat安装
        下载：
            链接: https://pan.baidu.com/s/1BgLpsNIpxt9Qa1msTWMI4g 提取码: vpsa
        配置:
            解压,复制解压文件到指定文件夹cmd
                cp ./navicat120_premium_cs_x64 /usr/local/tool/ -r
            创建桌面快捷方式cmd
                cd /usr/share/applications
                sudo gedit navicat.desktop
                   navicat.desktop内容:
                     [Desktop Entry]
                     Encoding=UTF-8
                     Name=navicat
                     Comment=The Smarter Way to manage dadabase
                     Exec=/usr/local/tool/navicat120_premium_cs_x64/start_navicat
                     Icon=/usr/local/tool/navicat120_premium_cs_x64/navicat-icon.png
                     Categories=Application;Database;MySQL;navicat
                     Version=1.0
                     Type=Application
                     Terminal=0   
            图标下载到navicat120_premium_cs_x64文件夹并重命名cmd
                wget http://www.navicat.com.cn/images/02.Product_00_AllProducts_Premium_large.png -O navicat-icon.png
        启动:
            首次启动提示mono和gecko安装,不安装也可以运行navicat.选择取消即可
   ![image](img/navicat-start-note.png)                  
## 12.安装mysql
    采用Docker方式安装
    docker pull mysql:5.7.29
    docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql:5.7.29
        	
## 图片涂抹工具安装
    image-edit-tool.png
