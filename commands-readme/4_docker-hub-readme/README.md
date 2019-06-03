# Docker hub commands

## Docker hub

#### 1. Docker Hub Repository作成 

```
# public(無料枠)で作成してください
https://hub.docker.com/
```

#### 2. Docker Login

```
$ docker login
Username: jeayoon
Password:
Email: 
WARNING: login credentials saved in /Users/kohei/.docker/config.json
Login Succeeded
```

#### 3. Docker image確認

```
$ docker image ls
```

#### 4. Docker Hub push 準備

```
# 例としてPHP(Dockerfileで作ったもの)をpushしてみましょ
$ docker tag {IMAGE_ID} {DOCKER_HUB_USERNAME}/{REPOSITORY_NAME}:{TAG}
```

#### 5. Docker push

```
# 例としてPHP(Dockerfileで作ったもの)をpushしてみましょ
$ docker push {DOCKER_HUB_USERNAME}/{REPOSITORY_NAME}
```

#### 6. Docker Hubにpushした container & image 削除

```
$ docker container rm {CONTAINER_NAME} -f
$ docker image rm {IMAGE_ID}
```

#### 7. Docker pull

```
$ docker pull {DOCKER_HUB_USERNAME}/{REPOSITORY_NAME}:{TAG}
```

#### 8. Docker network + Docker Hubにpushしたimageを起動

```
# 例としてPHP(Dockerfileで作ったもの)を起動してみましょ
$ docker container run -p 80:80 --mount type=bind,src={LOCAL_HOST_PATH},dst=/var/www/html --network {NETWORK_NAME} --name php -d {REPOSITORY_NAME}:{TAG}

```

#### 9. ブラウザで確認 (locakhost IP:port/info.php)

