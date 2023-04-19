# python-docker

自分用のPythonの開発環境用dockerfile

## 使い方

前提としてDocker Desktop for Macはインストール済みであること。M1以降のmacとかだと色々とゴニョゴニョする必要がある。

Dockerのインストールが完了しているのなら次のコマンドを叩いて **jupyter/scipy-notebook** のdockerイメージを仮想環境にダウンロードする。

    $ docker pull jupyter/scipy-notebook

使用したいプログラムなどが置いてあるディレクトリは **docker-compose.yml** の中のvolumesを変更してローカルのディレクトリを指定する。

    version: '3.8'

    services:
        jupyter:
            build: .
            ports:
                - "8888:8888"
        volumes:
                - ./notebooks:/home/jovyan/work

上記だとnotebooksのところを自分の環境に合わせる。

このリポジトリを設置してあるディレクトリで **docker-compose** で起動する。

    $ docker-compose up　-d --build

開発を行うときはvscodeの **Visual Studio Code Remote - Containers** を使ってimageをマウントする。終了するときは下記。

    $ docker-compose kill