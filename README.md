# env-ubuntu

## 目的

- テスト用の VMを virtualbox + vagrant で作成する

## 環境

- mac
- virtual box + vagrant
- linux

## ディレクトリ構成

概説

- vagrant 設定は `./vagrant` 配下に用意する

構成

- 最終的なディレクトリ構成

  ```bash
  .
  ├── README.md
  └── vagrant # vagrant関連の設定を格納
      └── centos7
          ├── .vagrant # vagrantコマンドで自動生成 (サブディレクトリは省略)
          └── Vagrantfile # vagrantコマンドで自動生成
  ```

## 手順

### 諸々のインストール

- virtual box

  ```terminal
  brew install --cask virtualbox
  ```

- vagrant

  ```terminal
  brew install --cask vagrant
  ```

### vagrant を利用し、virtual box 上に VM を作成する

- vagrant box を追加する
  <https://app.vagrantup.com/>からboxを検索する

  - centos/7

    ```bash
    vagrant box add centos/7
    ```

    provider を何にするか聞かれるので、`3) virtualbox`を選択する。

  - ubuntu

    ```bash
    vagrant box add ubuntu/focal64
    ```

  インストールした box を確認するときは

  ```bash
  vagrant box list
  ```

- ディレクトリ作成&移動する

  仮想マシン作成用のディレクトリ(`centos7`など)を作成し、Vagrantfile を作成する。

  ```bash
  mkdir vagrant/centos/7
  ```

  以下、`vagrant`コマンドはすべてVagrantfileが存在するディレクトリで実行する

- Vagrantfile を作成する

  ```bash
  vagrant init centos/7
  ```

  `config.vm.network "private_network"`の部分の設定は、バッティングしないよう適切な IP アドレスを設定する。

- VM を起動する

  ```bash
  vagrant up
  ```

- VM の状態を確認する

  ```bash
  vagrant status
  ```

- ssh で VM に接続する

  ```bash
  vagrant ssh
  ```

  素の ssh でログインするときは、下記を実行する。

  ```bash
  ssh -i [vagrantfileがあるディレクトリ]/.vagrant/machines/default/virtualbox/private_key vagrant@192.168.56.10
  ```

- VM をシャットダウンする

  ```bash
  vagrant halt
  ```