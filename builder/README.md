# AWX Docker

## はじめに

awx 関連でビルドに必要な情報を記載。
作ったコンテナは基本的にこちらにある

- [container置き場](https://github.com/ainamori?tab=packages)


## ファイル構成と使い方

### Docker-ansible-builder

- awx-eeを作るためのansible-builerイメージ作成用のDockerfile
  - [こちらのissue](https://github.com/ansible/ansible-builder/issues/447)に代表されるように、awx-eeのイメージとバージョンを合わせたリリースがなされていないようなので自分で管理する為の物


```bash
 docker build -f Dockerfile-ansible-builder -t ghcr.io/ainamori/ansible-builder:centos9 .
 docker push ghcr.io/ainamori/ansible-builder:centos9
```


### Docker-awx

- awx hybrid nodeのコンテナ作成用Dockerfile

```bash
 docker build -f Dockerfile-awx -t ghcr.io/ainamori/awx:devel .
 docker push ghcr.io/ainamori/awx:devel
```

### Docker-receptor

- awx receptor　nodeのコンテナ作成用Dockerfile
  - ただし、中身を見るとわかるがawxコードをマウントしていないだけでawxとほぼ同じ

```bash
 docker build -f Dockerfile-receptor -t ghcr.io/ainamori/awx-receptor:devel .
 docker push ghcr.io/ainamori/awx-receptor:devel
```

### Docker-awxkit

- awxコマンドを内包したもの。awxの実行には必須では無いがあると便利

```bash
 docker build -f Dockerfile-awxkit -t ghcr.io/ainamori/awxkit:devel .
 docker push ghcr.io/ainamori/awxkit:devel
```

### Docker-awxui

- awx-ui これだけはawxの方にDockerfileがある為、そちらを使う

```bash
 cd awx/ui
 docker build -f Dockerfile -t ghcr.io/ainamori/awx-ui:latest .
 docker push ghcr.io/ainamori/awx-ui:latest
```
