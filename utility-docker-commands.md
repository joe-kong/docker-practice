### 概要

プロジェクトでよく使われているDocker Commandを備忘録としてここでメモいたします。随時に更新していく予定です。

あくまで開発時に私個人がよく使うdockerコマンドですが。どなたかにお役に立てれば幸いです。



### コマンドメモ

###### Docker デーモンの起動

```shell
$ sudo systemctl start docker
# systemctlがないLinuxの場合
$ sudo service docker start
```

###### Docker デーモンの停止

```shell
$ sudo systemctl stop docker
# systemctlがないLinuxの場合
$ sudo service docker stop
```

###### Docker をブート時に自動起動する

```shell
$ sudo systemctl enable docker
# systemctlがないLinuxの場合
$ sudo chkconfig docker on
```

###### Dockerコマンドをsudoなしで実行する

```shell
$ sudo usermod -aG docker hogehoge.
```

###### Dockerイメージの取得

```shell
$ docker pull [image]:[version] 
```

###### Dockerコンテナの起動

```shell
$ docker start [image]:[version] [コマンド]
```

###### Dockerイメージの取得~コンテナの起動の一括実行

```shell
$ docker run [オプション] [image]:[version] 
# [--name]オプションで起動するコンテナに名前を付けることができる。
# [-itd]オプションでデタッチ状態でコンテナのbashを起動。
```

###### Installed Dockerイメージリストの確認

```shell
$ docker images
```

###### 実行中のコンテナの確認

```shell
$ docker ps

# 以下の項目が表示される
# CONTAINER ID  IMAGE  COMMAND     CREATED    STATUS    PORTS     NAMES
```

###### 全てのコンテナの確認

```shell
$ docker ps -a
# -q(--quite)を指定するとcontainerIDのみが出力
$ docker ps -qa
```

###### 起動しているコンテナの停止

```shell
$ docker stop [コンテナID]
$ docker stop [コンテナ名]
```

###### 起動しているコンテナの再起動

```shell
$ docker restart [コンテナID]
$ docker restart [コンテナ名]
```

###### Dockerコンテナの自動起動設定

```shell
$ docker update --restart=always [コンテナ名]
```

###### コンテナの削除

```shell
$ docker rm [オプション] [コンテナID]
$ docker rm [オプション] [コンテナ名]
# 強制に削除する場合、-f(force) オプションを使う
```

###### インストールされているdockerイメージの削除

```shell
$ docker rmi [イメージ名]
# イメージが起動中のコンテナで使用されている場合は削除できないので。コンテナを事前に削除する必要がある
$ docker rmi `docker images` # すべてのDockerイメージを一括削除したい場合
```

###### 指定コンテナ/イメージに関する全ての情報を取得する

```shell
$ docker inspect [オプション] [イメージ名|イメージID｜コンテナ名｜コンテナID]
# オープションがないと全ての情報が一気に出力され、読みにくいです。必要な情報のみを出力するオプションをつけるのが一般的です。
# ログパス取得する場合
$ docker inspect --format='{{.LogPath}}' [コンテナID]
# grepでもよい
$ docker inspect {docker_id} | grep 'LogPath'
```




