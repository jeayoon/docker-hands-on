# MySQL commands

## Docker MySQL

#### Docker MySQL 構成図

![mysql_docker](https://user-images.githubusercontent.com/17561411/58700871-52667180-83dc-11e9-9b59-a4632cd66c1d.png)

#### 1. pull MySQL5.7

```
$ docker image pull mysql:5.7
```

#### 2. MySQL5.7 images確認

```
$ docker image ls
```

#### 3. 初期データ投入を準備 

```
# 好きな場所でOK
$ mkdir /docker/mysql/init

# ~.sql OR ~.gzで作成する必要がある
$ vi /docker/mysql/init/initial_db.sql

CREATE DATABASE test;
USE test;
CREATE TABLE test(name VARCHAR(100));
INSERT INTO test VALUES('jy_jeong');

```

#### 4. 初期データ投入をBind mountで起動する

```
# HostのディレクトリをContainerのディレクトで利用できるようにmountする

$ docker container run --mount type=bind,src=/docker/mysql/init,dst=/docker-entrypoint-initdb.d -p 4306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=fusic -d mysql:5.7

```
- --mount : type=bind,src={HostのディレクトリPath},dst={ContainerのディレクトPath}
- -p : -p {ホスト側のポート}:{コンテナのポート} 
- --name : Container名
- -d : ContainerがBackgroundで実行

#### 5. MySQL5.7 container 操作
```
$ docker container exec -it {containerID or NAMES} bash
```

#### 6. 初期データ投入されたのかを確認
```
$ mysql –p{PW}
mysql > USE test;
mysql > SELECT * FROM test;
+---------+
| name     |
+---------+
| jy_jeong |
+---------+
```

#### 7. exitで docker clientに移動してください

#### 8. Volume mountのために MySQL containerを削除する
```
# -fで強制的にcontainerを全部削除
$ docker container rm {containerID or NAMES} -f 
               
                or
               
# 実行中のcontainerをstop
$ docker container stop {containerID or NAMES}

# 停止中のcontainer一覧
$ docker container ls -a

# 停止中のcontainer削除
$ docker container rm {containerID or NAMES}         
               
```
#### 9. Volume作成
```
$ docker volume create {VOLUME_NAME}
```

#### 10. Volume一覧
```
$ docker volume ls
```

#### 11. Volume削除
```
$ docker volume rm {VOLUME_NAME}
```

#### 12. BindとVolume Mount設定して起動
```
# Docker Host内にContainerとVolumeを繋げて永続化する
$ docker container run --mount type=bind,src={LOCAL_HOST_PATH},dst=/docker-entrypoint-initdb.d --mount type=volume,src={VOLUME_NAME},dst=/var/lib/mysql -p 4306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=fusic -d mysql:5.7

```
- --mount : type=volume,src={VOLUME NAME},dst=/var/lib/mysql

#### 13. MySQL5.7 container 操作
```
$ docker container exec -it {containerID or NAMES} bash
```

#### 14. 初期データ投入されたのかを確認
```
$ mysql –p{PW}
mysql > USE test;
mysql > SELECT * FROM test;
+---------+
| name     |
+---------+
| jy_jeong |
+---------+
```

#### 15. 初期データを投入せずに、Volume Mountだけ繋げて、データ永続化を確認する
```
# containerを全部削除(Volume Mountだけ繋げるために)
$ docker container rm {containerID or NAMES}

# Volume Mountでrun
$ docker container run --mount type=volume,src={VOLUME_NAME},dst=/var/lib/mysql -p 4306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=fusic -d mysql:5.7

$ docker container exec -it {containerID or NAMES} bash

$ mysql –p{PW}
mysql > USE test;
mysql > SELECT * FROM test;
+---------+
| name     |
+---------+
| jy_jeong |
+---------+
```
