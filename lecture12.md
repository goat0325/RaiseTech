# 第１２回課題

## 課題内容
1. 提供されたcircleciのサンプルコンフィグが、正しく動作するようにリポジトリに組み込む。動作ができたら報告。

### 1.  circleciとは

SaaS（Software as a Service）型のCI/CDツール。

無料枠あり。


### 2. SaaSとは
```
サービス提供事業者（サーバー）側で稼働しているソフトウェアを、インターネットなどのネットワークを経由して、ユーザーが利用できるサービス。一般的に、SaaSは提供されるソフトウェアを指す。
```

### 3. CI/CDツールとは

- CI/CDツールとは

```
「Continuous Integration/Continuous Delivery」の略称。
→継続的な価値提供、継続的なリリースを維持するもの。

・CI（継続的インテグレーション）・・・
アプリケーションやインフラ環境のコードに関わる部分のテストを自動化し、常にリリース可能な状態にすること。

・CD（継続的デリバリー）・・・
リリース可能な状態にするだけでなく、リリースまで行うケース。

→CI/CDはやる事や目的はほぼ同じ、どこまでやるかだけが違う。
circleciは、いくつかあるCI/CDツールの中の一つ。
```

- CI/CDツールの機能

以下の機能を使い、自動的にテストを実装したり、リリースしたりする。
- ジョブ機能：定形作業を自動化した小さな単位＝ジョブとする。

- トリガー機能：ジョブはただ実行されるだけではなく、トリガーを設定することで、起動条件を詳細に指定できる。
例）前のジョブが完了したら実行する。
　　指定の時間が来たら定期的に実行する。など

- パイプライン機能：ジョブ機能・トリガー機能を一連の流れ（パイプライン）とすることで、呼び出す時の記述が容易になる、全体の可視化がしやすくなる。



## 1. circleciのサンプルコンフィグの動作確認

- circleciディレクトリ、config.ymlファイルを作成しgithubへpush
```
$ mkdir .circleci
$ cd .circleci
$ touch config.yml
$ cd
$ cd RaiseTech
$ git add .circleci/config.yml
$ git commit -m "Add CircleCI configuration file"
$ git push origin main
```

サンプルを参考に動作を確認していく
- [circleciサンプル](yaml/lecture12/sample-lecture12-config.yml)


以下サンプルの内容
```
version: 2.1    #circleciの設定ファイルのバージョン
orbs:           #pythonの実行環境を設定。python用のorbを使用。
  python: circleci/python@2.0.3
jobs:           
  cfn-lint:   #ジョブの名前
    executor: python/default   #pythonのデフォルト実行環境を使用
    steps:
      - checkout   #リポジトリのチェックアウト（gitリポジトリからソースコードや設定ファイルなどのファイルを取得すること。これにより、circleciが指定されたジョブを実行するためのコードベースを取得できる。）
      - run: pip install cfn-lint   #cfn-lintをインストール
      - run:
          name: run cfn-lint
          command: |
            cfn-lint -i W3002 -t cloudformation/*.yml   #cfn-lintジョブを実行して、cloudformationテンプレートの構文エラーやベストプラクティスに準拠しているかをチェック

workflows:   #ワークフローを定義
  raisetech:
    jobs:
      - cfn-lint
```

### test10にて作成したYAMLファイルを使用してテスト実行

※今回の課題では、lecture10で作成した「test10-vpc.yml」をコピーし、「copy-test10-vpc.yml」としてimg/lecture12に保存したものをテストに使用。

- [元々作成していたtest10-vpc.yml](./img/lecture10/test10-vpc.yml)

上記記載のcircleciのサンプルコードを使用してテストを実行。

表示されたエラー画像
![エラー１](img/lecture12/12-1%20cfn-lint%20error1.png)
![エラー２](img/lecture12/12-2%20cfn-lint%20erroe2%20cloudformationファイルないよ.png)
cloudformation/*.ymlというパスに対応するファイルが存在しないというエラーが出る。


- ymlファイルがあるファイルを指定
```
.circleci/config.yml内を編集

●変更前
jobs:
  cfn-lint:
    steps:
    ~
    ~
    - run:
        name: run cfn-lint
        command: |
          cfn-lint -i W3002 -t cloudformation/*.yml

●変更後
~
~
command: |
  cfn-lint -i W3002 -t yaml/lecture12/*.yml


これで、yaml/lecture12内にあるymlファイルを参照するように設定。
```

表示されたエラー画像
![エラー３](img/lecture12/12-3%20erroe3.png)

記載されているエラー内容

#### 1. W3010：警告コード

#### 2. Don't hardcode ap-northeast-la(1c) for AvailabilityZones
特定のルールに違反している。今回は、アベイラビリティゾーンをハードコード（直書き）してしまっていることが問題。

#### 3. img/lecture12/copy-test10-vpc. yml: 45:7
エラーが見つかったファイルとその行番号、列番号


- copy-test10-vpc.yml内のAvailabilityZonesを確認
```
●変更前
アベイラビリティゾーンに関して、
Parametersブロックには記載なし。
Resourcesブロック内には直書きしていたため、
Parametersブロックに記載し、それを参照するように変更。


●変更後
==============================================
Parameters:
~
~
  MyAvailabilityZone1:
    Description: Availability Zone for Public Subnet 1
    Type: String
    Default: ap-northeast-1a
  
  MyAvailabilityZone2:
    Description: Availability Zone for Public Subnet 2
    Type: String
    Default: ap-northeast-1c
===============================================


Resources:
===========================
# パブリックサブネットを２つ作成
===========================

  MyPublicSubnet01:
    ~
      AvailabilityZone: !Ref MyAvailabilityZone1
    ~
    ~

  MyPublicSubnet02:
    ~
      AvailabilityZone: !Ref MyAvailabilityZone2
    ~
    ~

=============================
# プライベートサブネットを２つ作成
=============================

  MyPrivateSubnet01:
    ~
      AvailabilityZone: !Ref MyAvailabilityZone1
    ~
    ~

  MyPrivateSubnet02:
    ~
      AvailabilityZone: !Ref MyAvailabilityZone2
    ~
    ~
================================================
```

変更後、再度circleciテスト実行
![テスト成功](img/lecture12/12-4%20success.png)