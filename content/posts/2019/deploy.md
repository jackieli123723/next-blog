---
title: 与Docker PM2 部署 next.js 
date: 2019-11-19
---




## $$
to run npm start with pm2-docker inside the container below command worked for me

CMD ["pm2-docker", "npm", "--", "start"]


docker 

### CMD [ "pm2-runtime", "start", "npm", "--", "start" ] vs CMD ["npm","run","start:prod"]


### "start:prod": "pm2-docker start ./pm2_config.json" 安装 

 "dependencies": {
    
    "pm2": "^2.10.2",

  },


## vultr 服务器 

+ express@4.17.1
added 50 packages from 37 contributors and audited 126 packages in 2.271s
found 0 vulnerabilities

[root@west demo]# node server.js 
Example app listening on port 3000!
访问不到 

无法访问此网站149.28.189.252 的响应时间过长。


## docker启动 访问的到 (一句话原则vultr 服务器  用docker启动 可以启动服务 )



http://149.28.189.252:8086/ 、、hello-vue


[root@west demo]# docker run -p 8086:8081 -d hello-vue 
Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
160bd3e4751dcf8a95eaa5d141703e6b5a295789537f45542a43f6afd76e5da9
[root@west demo]# docker images
Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
REPOSITORY                              TAG      IMAGE ID       CREATED         SIZE
docker.io/jackieli123456/hello-vue      latest   dcc402f6640c   17 months ago   704 MB
docker.io/letssudormrf/ssr-bbr-docker   latest   241bedc074a1   2 years ago     287 MB
[root@west demo]# docker ps
Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
CONTAINER ID  IMAGE                                         COMMAND               CREATED         STATUS             PORTS                                           NAMES
160bd3e4751d  docker.io/jackieli123456/hello-vue:latest     npm start             12 seconds ago  Up 12 seconds ago  0.0.0.0:8086->8081/tcp                          vigorous_davinci
f908fe2a7bd6  docker.io/letssudormrf/ssr-bbr-docker:latest  /root/start.sh -p...  43 hours ago    Up 43 hours ago    0.0.0.0:6567->6567/tcp, 0.0.0.0:6567->6567/udp  ssr-bbr-dockere
d494255be53e  docker.io/letssudormrf/ssr-bbr-docker:latest  /root/start.sh -p...  43 hours ago    Up 43 hours ago    0.0.0.0:5567->5567/tcp, 0.0.0.0:5567->5567/udp  ssr-bbr-dockers
3a51cc4a6185  docker.io/letssudormrf/ssr-bbr-docker:latest  /root/start.sh -p...  43 hours ago    Up 43 hours ago    0.0.0.0:4567->4567/tcp, 0.0.0.0:4567->4567/udp  ssr-bbr-docker


##
---
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(8081, function () {
  console.log('app listening on port 8081!')
})

Dockerfile

FROM node:7
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
CMD node index.js
EXPOSE 8082
----


 docker build -t hello-vue .
 docker run -p 8082:8081 hello-vue
 
 

to run npm start with pm2-docker inside the container below command worked for me


配合 RUN npm install pm2 -g || RUN npm install --global pm2

CMD ["pm2-docker", "npm", "--", "start"]


### pm2 镜像有node环境？

pm2 runtime是一个替换node.js二进制文件，具有一些有趣的生产特性

>>> pm2-runtime -h

  Usage: pm2-runtime app.js

  pm2-runtime is a drop-in replacement node.js binary with some interesting production features


###https://github.com/keymetrics/doc-pm2/blob/6783150d91298fe1f2e50113cfdc3421395dc93f/zh/runtime/integration/docker.md

与Docker一起使用PM2
生产就绪的Node.js Docker镜像，包括 PM2。

pm2-runtime的目标是将您的应用包装到合适的Node.js生产环境中。 它解决了在容器内部运行Node.js应用时遇到的主要问题：

高应用可靠性的第二个过程回退
进程流控制
自动监控应用以便使它始终保持健全和高性能
自动源地图发掘与解析支持
除此之外，使用PM2作为容器和应用之间的一个层，带来了PM2强大的功能，如生态系统文件，自定义日志系统和pm2的其他功能。

 ###？？？CMD [ "pm2-runtime", "start", "ecosystem.config.js" ]
 设置一个Docker文件
使用以下内容创建一个名为Dockerfile的新文件

FROM keymetrics/pm2:latest-alpine

# Bundle APP files
COPY src src/
COPY package.json .
COPY ecosystem.config.js .

# Install app dependencies
ENV NPM_CONFIG_LOGLEVEL warn
RUN npm install --production

# Expose the listening port of your app
EXPOSE 8000

# Show current folder structure in logs
RUN ls -al -R

CMD [ "pm2-runtime", "start", "ecosystem.config.js" ]


建立您的镜像
从您的Node.js应用项目文件夹启动这些命令：

docker build -t your-app-name .
运行您的镜像
docker run -p 80:8000 your-app-name
-p 80:8000将您应用的端口8000绑定到本地主机的端口80 {: .tip}

pm2命令
pm2命令仍然可以在docker exec命令的容器中使用：

# Monitoring CPU/Usage of each process
docker exec -it <container-id> pm2 monit
# Listing managed processes
docker exec -it <container-id> pm2 list
# Get more information about a process
docker exec -it <container-id> pm2 show
# 0sec downtime reload all applications
docker exec -it <container-id> pm2 reload all
暴露安全端点
CMD ["pm2-runtime", "ecosystem.config.js", "--web"]
--web [port]选项允许通过JSON API公开所有重要信号（docker实例+应用）.

在shell中安装pm2之后，运行 pm2-runtime -h获取所有可用选项. {: .tip}

您准备好了
就是这样！ 您的容器已准备好部署。

下一步

###deploy 
RUN npm install --global pm2
RUN npm install --production

# Build app
RUN npm run build:content && npm run build


# Install dependencies
RUN npm install --production


 --production？  不安装  devDependencies 
  "devDependencies": {
    "next": "^9.1.0",
    "processmd": "^4.5.0",
    "standard": "^14.3.1"
  },
  "dependencies": {
    "react": "^16.10.2",
    "react-dom": "^16.10.2",
    "styled-jsx": "^3.2.2"
  }

> next-blog@3.2.0 build:content /app
> processmd content/**/*.md --outputDir content --preview 110 --summaryOutput content/summary.json

sh: 1: processmd: not found
npm ERR! code ELIFECYCLE
npm ERR! syscall spawn
npm ERR! file sh
npm ERR! errno ENOENT
npm ERR! next-blog@3.2.0 build:content: `processmd content/**/*.md --outputDir content --preview 110 --summaryOutput content/summary.json`
npm ERR! spawn ENOENT
npm ERR! 
npm ERR! Failed at the next-blog@3.2.0 build:content script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
ERRO[0002] read container terminal output: input/output error: input/output error 

npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2019-10-16T03_12_21_127Z-debug.log
error building at step {Env:[PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin NODE_VERSION=12.12.0 YARN_VERSION=1.19.1] Command:run Args:[npm run build:content && npm run build] Flags:[] Attrs:map[] Message:RUN npm run build:content && npm run build Original:RUN npm run build:content && npm run build}: error while running runtime: exit status 1
[root@west next-blog]# 

> next-blog@3.2.0 build /app
> next build

sh: 1: next: not found
npm ERR! code ELIFECYCLE
npm ERR! syscall spawn
npm ERR! file sh
npm ERR! errno ENOENT
npm ERR! next-blog@3.2.0 build: `next build`
npm ERR! spawn ENOENT
npm ERR! 
npm ERR! Failed at the next-blog@3.2.0 build script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
ERRO[0001] read container terminal output: input/output error: input/output error 

npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2019-10-16T03_19_38_927Z-debug.log
error building at step {Env:[PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin NODE_VERSION=12.12.0 YARN_VERSION=1.19.1] Command:run Args:[npm run build] Flags:[] Attrs:map[] Message:RUN npm run build Original:RUN npm run build}: error while running runtime: exit status 1
[root@west next-blog]# 


### 安装pm2 到自身package.json 
lenovo@lenovo-PC MINGW64 /e/jackieli/react-day-to-day/next-ssr/next-blog (master)
$ yarn run start:prod
yarn run v1.10.1
$ pm2-docker start ./ecosystem.json
[WARN] PM2 Daemon is already running
> Ready on http://localhost:3000


lenovo@lenovo-PC MINGW64 ~/Desktop
$ pm2 ls
┌─────────────────────┬────┬─────────┬─────────┬───────┬─────────┬─────────┬────────┬─────┬───────────┬────────┬──────────┐
│ App name            │ id │ version │ mode    │ pid   │ status  │ restart │ uptime │ cpu │ mem       │ user   │ watching │
├─────────────────────┼────┼─────────┼─────────┼───────┼─────────┼─────────┼────────┼─────┼───────────┼────────┼──────────┤
│ server              │ 0  │ 3.2.0   │ fork    │ 0     │ stopped │ 0       │ 0      │ 0%  │ 0 B       │ lenovo │ disabled │
│ west-next-blog-prod │ 1  │ 3.2.0   │ cluster │ 14608 │ online  │ 0       │ 32s    │ 0%  │ 28.5 MB   │ lenovo │ disabled │
└─────────────────────┴────┴─────────┴─────────┴───────┴─────────┴─────────┴────────┴─────┴───────────┴────────┴──────────┘
 Use `pm2 show <id|name>` to get more details about an app

lenovo@lenovo-PC MINGW64 ~/Desktop
$



#### Dockerfile 启动 node 

CMD ["node","server.js"] ok
CMD ["pm2-docker", "npm", "--", "start"] ???  --ok   ===等价于 CMD pm2-docker start npm -- start
#CMD [ "pm2-runtime", "start", "npm", "--", "start" ] ok 
CMD ["npm","run","start:prod"] ok
CMD [ "npm", "start" ] ok

CMD [ "pm2-runtime", "start", "ecosystem.config.js" ] ok
CMD [ "pm2-runtime", "start", "ecosystem.json" ]


###
FROM node:carbon  
  
# Create app directory  
WORKDIR /usr/src/app  
  
# A wildcard is used to ensure both package.json AND package-lock.json are
copied  
COPY package*.json ./  
  
# Install app dependencies  
RUN npm install --only=production  
  
# Install the pm2-docker programm  
RUN npm install pm2 -g  
  
# Bundle app source  
COPY . .  
  
# Create our frontend build  
RUN npm run build  
  
# Expose the port node listens to  
EXPOSE 3000  
# Remove some build files  
RUN rm -rf webpack.config.js frontend.js package*.json  
  
# Start the app  
CMD [ "pm2-docker", "--optimize_for_size", "--max_old_space_size", "460", "--
gc_interval", "100", "ecosystem.json" ]  


##pm2 分割日志 dockerfile 

RUN npm i

# 分割日志
# RUN pm2 install pm2-logrotate
# RUN pm2 set pm2-logrotate:compress true

# 拷贝源代码(ecosystem.config.js)到docker工作目录
COPY ./ ./

EXPOSE 8080


###



### next docker  pm2-runtime部署测试  


[root@west next-blog]# docker build -t west-next-blog-pm2-runtime .

docker run -p 13091:3000 west-next-blog-pm2-runtime 

docker run -p 13091:3000  -d west-next-blog-pm2-runtime 




## 占用内存？？？



# Show current folder structure in logs
RUN ls -al -R

####

内存不够  


npm WARN deprecated flatten@1.0.2: I wrote this module a very long time ago; you should use something else.
[        ..........] - extract:@webassemblyjs/helper-wasm-bytecode: http fetch
fatal error: runtime: out of memoryhttp fetch GET 200 https://registry.npmjs.or

runtime stack:
runtime.throw(0x556500ca007b, 0x16)
	/usr/lib/golang/src/runtime/panic.go:608 +0x74 f
	#加入以下3条命令去释放cache/buff
[root@DD-Server-9F ~]# echo 1 > /proc/sys/vm/drop_caches
[root@DD-Server-9F ~]# echo 2 > /proc/sys/vm/drop_caches
[root@DD-Server-9F ~]# echo 3 > /proc/sys/vm/drop_caches
[root@DD-Server-9F ~]# free -h
              total        used        free      shared  buff/cache   available
Mem:           7.7G        1.3G        6.0G        376M        479M        5.8G
Swap:          8.0G          0B        8.0G
如果想自动释放，可以加入crontab计划任务处理，或者写个自动化脚本去执行，效果会更显著。


	
docker stop 容器id 
docker restart 容器id


docker  stop ede7c446c313


