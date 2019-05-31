# PHP commands

## Docker PHP

#### Docker php 構成図



#### 1. pull PHP7.3

```
$ docker image pull php:7.3-apache
```

#### 2. php7.3 image確認
```
$ docker image ls
```

#### 3. php7.3起動
```
$ docker container run -p 80:80 --mount type=bind,src={LOCAL_HOST_PATH},dst=/var/www/html --name php -d php:7.3-apache
```
- -p : -p {ホスト側のポート}:{コンテナのポート}
- --mount : type=bind,src={HostのディレクトリPath},dst={ContainerのディレクトPath}    
HostのディレクトリをContainerのディレクトで利用できるようにmountする
- --name : Container名
- -d : ContainerがBackgroundで実行

#### 4. 稼働中のPHP7.3 container確認
```
$ docker container ls
```

#### 5. Mount設定した場所にphpinfo()作成
```
$ vi info.php 
<?=phpinfo();?>
```

#### 6. PHP7.3 container 操作
```
$ docker container exec -it {containerID or NAMES} bash
```
- exec : 対象のコマンドを実行する
- -i : 標準入力を開き続ける(Keep STDIN open even if not attached) 
- -t : 疑似tty(CLI)を割りあてる(Allocate a pseudo-TTY)

#### 7. ブラウザー確認
```
locahost:port/info.php
```