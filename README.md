
#依次运行以下命令，安装jd_v4和面板。


1、安装v4_bot(amd64) 一键命令（1）

  (如是群晖用户，提前在docker下新建文件夹jd，下面再新建config，log，own，diy，scripts五个文件夹，左边路径改为实际的绝对路径。)
  
  (强烈建议：自行修改本地宿主机端口，即修改左边的5678)
  
    docker run -dit \
    -v /jd/config:/jd/config \
    -v /jd/log:/jd/log \
    -v /jd/own:/jd/own \
    -v /jd/diy:/jd/jbot/diy \
    -v /jd/scripts:/jd/scripts \
    -p 5678:5678 \
    -e ENABLE_HANGUP=true \
    -e ENABLE_WEB_PANEL=true \
    --name jd \
    --hostname jd \
    --restart always \
    qianyi09/jd:latest



1.1、安装v4_bot(amd64) 一键命令（2）

    wget -q https://raw.githubusercontent.com/qianyi09/jd_v4/main/jd-docker.sh -O jd-docker.sh && chmod +x jd-docker.sh && ./jd-docker.sh


   
2、进入容器，默认容器名jd，如做了修改，按实际修改命令。

    docker exec -it jd bash 


 
3、安装面板，已去除ttyd终端，(切记先要进入容器再执行)。

   执行以下命令后，请访问5678端口进行配置，如果你做了修改，请使用实际端口进行访问，默认用户名admin，密码adminadmin。
   
   （强烈建议：仅本地使用面板，非要远程可路由开启VPN回家。）
 
    wget -q https://raw.githubusercontent.com/qianyi09/jd_v4/main/v4mb.sh -O v4mb.sh && chmod +x v4mb.sh && ./v4mb.sh
 



4、镜像默认用我的库作为主库，三方库自行添加。装好更新后，安装新版宠汪汪的依赖：

 （先进入容器，参考第2条。再依次执行以下3条命令。）

    apk add --no-cache build-base g++ cairo-dev pango-dev giflib-dev

    cd scripts

    npm install canvas --build-from-source



5、如不想用我的库，阻止主库更新后，当脚本报错缺少依赖时，依次执行以下3条命令，默认容器名jd，如做了修改，按实际修改命令。

  (前提scripts文件夹里得有package.json，没有就去我scripts库里找)

    docker exec -it jd bash
    cd scripts
    npm install
