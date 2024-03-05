1. 新建文件夹并进入 用于放文件

2. 下载node的压缩包 https://downloads.apache.org/

   wget https://downloads.apache.org/maven/maven-3/LATEST/binaries/apache-maven-3.6.3-bin.tar.gz

3. 解压apache-maven-3.6.3-bin.tar.gz

   解压完之后进入bin目录内使用mvn -v 查看版本

4. 配置全局环境变量

   进入/etc/profile文件在最后添加

   export MAVEN_HOME=路径

   PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH

5. source /etc/profile加载文件