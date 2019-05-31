# PHP-MySQL commands

## PHP-MySQL連携

#### Docker PHP-MySQ 構成図

![mysql_docker](https://user-images.githubusercontent.com/17561411/58700871-52667180-83dc-11e9-9b59-a4632cd66c1d.png)

#### 1. 前作業したcontainerを全部削除する

```
$ docker container rm {containerID or NAMES} -f
```

#### 2. Docker file 作成(phpのmysql拡張)

```
#好きな場所でOK
$ mkdir docker-info

$ vi docker-info/Dockerfile

FROM php:7.3-apache
RUN apt-get update && docker-php-ext-install pdo_mysql mysqli mbstring
```

#### 3. Docker image 作成

```
$ docker image build -t php:custom .
```
- -t : Tag設定。DockerHubの{imageName}:{TagName}
- . : Dockerfile Path設定(Dockerfile場所の上に設定すると 「.」になる)

#### 4. Docker network 作成

```
$ docker network create {NETWORK_NAME}
```

#### 5. Docker network 一覧

```
$ docker network create ls
```

#### 6. Docker network + php:customを起動

```
$ docker container run -p 80:80 --mount type=bind,src={LOCAL_HOST_PATH},dst=/var/www/html --network {NETWORK_NAME} --name php -d php:custom
```
- --network : Docket networkを設定する –network {NAME}

#### 7. Docker network + MySQLを起動

```
$ docker container run --mount type=volume,src={VOLUME_NAME},dst=/var/lib/mysql --name mysql --network {NETWORK_NAME} -p 4306:3306 -e MYSQL_ROOT_PASSWORD=fusic -d mysql:5.7
```

#### 8. network確認

```
$ docker network inspect {NETWORK_NAME}
```

#### 9. Docker network 確認
```
$ docker network inspect {NETWORK_NAME}
```

#### 10. PHPにDB情報出力
```
$ vi {LOCAK_HOST_PATH}/info.php

<meta charset="UTF-8">
<title>テスト</title>
<?php
$db = new PDO('mysql:host={MYSQL_CONTAINER_NAME};dbname={DB_NAME}', 'root', '{PASSWORD}');
$db->query("INSERT INTO test VALUES('ジョン')");
$st = $db->query("SELECT * FROM test");
var_dump($st->fetchAll());

```

#### 11.ブラウザで確認 (locakhost IP:port/info.php)

