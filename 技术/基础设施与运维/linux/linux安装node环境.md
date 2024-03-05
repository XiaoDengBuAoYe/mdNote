

node自带npm

1. 新建文件夹并进入 用于放文件

2. 下载node的压缩包 https://nodejs.org

   wget https://nodejs.org/dist/v16.20.2/node-v16.20.2-linux-x64.tar.xz

3. 解压 tar -xvf node-v16.20.2-linux-x64.tar.xz

   解压完之后进入bin目录内使用node -v 查看版本

4. 配置全局环境变量

   进入/etc/profile文件在最后添加

   export NODE_HOME=/nodejs路径

   export PATH=$PATH:$NODE_HOME/bin 

   export NODE_PATH=$NODE_HOME/lib/node_modules

5. source /etc/profile加载文件