# go4cron


## Overview

**go4cron**, golang 实现的crontab配置服务，支持到秒级控制 *linux crontab 服务*.

### Syntax

#### crontab配置表达式

字段   | 必须 | 值范围  | 允许字符
	----------   | ---------- | --------------  | --------------------------
	秒      | Yes        | 0-59            | * / , -
	分      | Yes        | 0-59            | * / , -
	小时        | Yes        | 0-23            | * / , -
	天 | Yes        | 1-31            | * / , - ?
	月        | Yes        | 1-12  | * / , -
	每周几天  | Yes        | 0-6  | * / , - ?

#### 配置实例

```
   * * * * * * /bin/sh /var/www/daemon/app/add_tag_from_search.sh > /alidata/logs/daemon/add_tag_from_search.log 每秒钟执行该脚本

   */5 * * * * * /bin/sh /var/www/daemon/app/queue.sh /dev/null 2>&1 & 每5秒钟执行脚本

   0 */5 * * * * /bin/sh /var/www/daemon/app/queue.sh /dev/null 2>&1 & 每5分钟执行脚本

   0 */5 20,21 * * * /bin/sh /var/www/daemon/app/queue.sh /dev/null 2>&1 & 20点和21点每5分钟执行脚本

   0 0 5 * * * /bin/sh /var/www/daemon/app/queue.sh /dev/null 2>&1 & 每天5点执行脚本

```

#### 使用方法

```
	A. centos首次使用安装go1.5，并设置GOPATH, GOROOT，以及工作目录

		1. cd /tmp

		2. wget http://www.golangtc.com/static/go/go1.5rc1/go1.5rc1.linux-amd64.tar.gz

		3. tar zxvf go1.5rc1.linux-amd64.tar.gz -C /usr/local

		4. 建立go工作目录:

			mkdir -p /home/go

			mkdir -p /home/go/src

			mkdir -p /home/go/bin

		5. vim /etc/profile 添加三行

			export GOROOT=/usr/local/go
			export GOBIN=$GOROOT/bin
			export GOPATH=/home/go
			export PATH=$PATH:$GOBIN:$GOPATH

		6. source /etc/profile

		7. go version

	B. 安装go4cron

		1. cd /home/go/src

		2. git clone git@github.com:yybirdcf/go4cron.git

		3. cd go4cron

		4. ./dependencies.sh

		5. go install

```
