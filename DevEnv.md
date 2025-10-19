- 本地创建运行RedashServer容器 
  - `container create --name redash -p 5001:5000 -e REDASH_COOKIE_SECRET=123ABC -e REDIS_URL=redis://:redis@192.168.64.1:6379/0 -e DATABASE_URL=postgres://postgres:postgres@192.168.64.1:5432/postgres redash:master`

- 本地创建初始化环境容器，如初始化数据库命令的运行
  - `container run -it --remove -p 5001:5000 -e REDASH_COOKIE_SECRET=123ABC -e REDIS_URL=redis://:redis@192.168.64.1:6379/0 -e DATABASE_URL=postgres://postgres:postgres@192.168.64.1:5432/postgres redash:master /bin/bash`

- 本地构建前端项目的容器
  - `container create -it -c 4 -m 6G --name node18 --volume ${HOME}:/root/host node:18-bookworm /bin/bash`
- 本地构建前端项目的命令
  ```bash
  # 设置代理环境变量
  export http_proxy=http://192.168.64.1:7890
  export all_proxy=socks5://192.168.64.1:7890
  
  # 跳过不必要的二进制下载
  export CYPRESS_INSTALL_BINARY=0
  export PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=1
  
  # 安装 Yarn
  npm install --global --force yarn@1.22.22
  
  # 安装依赖
  yarn --frozen-lockfile --network-concurrency 1 --verbose
  
  # 构建项目
  yarn build
  ```

 