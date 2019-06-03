# Hello world commands

## Docker Hello world

#### Docker Hello world 構成図

![hello-world-readme](https://user-images.githubusercontent.com/17561411/58769469-6976b080-85e2-11e9-9457-a7b3b7e9fb3c.png)

#### 1. pull Hello world

```
$ docker image pull hello-world
```

#### 2. Hello world image確認
```
$ docker image ls
```

#### 3. Hello world 実行
```
$ docker container run hello-world
```

#### 4. 実行したら、メッセージが表示されるのを確認
```
$ Hello from Docker!..
```

#### 5. 起動中のcontainer確認
```
$ docker container ls
```

#### 6. 停止中のcontainer確認
```
$ docker container ls -a
```

#### 7. 停止中のcontainer削除
```
$ docker container rm {container ID or NAMES)
```

#### 8. Docker images 削除
```
$ docker image rm {container ID}
```
