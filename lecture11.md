# 第11回課題

## 課題内容
1. serverspecのテスト成功
    - テストコードの中身は自由に

## 1. serverspecのテスト成功

### sereverspecについて

- serverspecとは・・・
```
Ruby で作成されたインフラ環境をテストする為のテスト用フレームワーク。

サーバーに対して
・特定のモジュールがインストールされているか
・ポートが開いているか
・任意のファイルが存在するか
といったサーバーの環境構成に関わるテストが記述でき、その記述のサポートをしてくれるフレームワークとなっている。
```

### serverspecを起動

第5回課題で作成したアプリケーションを利用してテストを行う

※serverspecをインストールする際にはRubyをインストールしている必要あり。
先にRubyを使えるように設定をしているか確認。

- serverspecインストール
```
ec2-user配下でインストール
$ gem install serverspec
```

インストール後
```
# serverspecのテスト環境を初期化する時のコマンド
$ serverspec-init

入力すると選択肢が表示される

Select OS type:　　　　　　# 利用しているOSを選択
1) UN*X
2) Windows
Select number: 1
Select a backend type:　　# テストの実行方法を選択
1) SSH
2) Exec (local)
Select number: 2

+ spec/ 
+ spec/www.example.jp/ 
+ spec/www.example.jp/sample_spec.rb
+ spec/spec_helper.rb
+ Rakefile + .rspec

今回は、OSは1、テストの実行方法は2を選択。
選択すると、ec2-user配下に新たにspecディレクトリが作成されている。
```

- テストコードを記述

テストコードは「sample_spec.rb」を編集、記述していく。元々記載されている記述は消さなくてOK。
```
# local環境にてテストを実行
$ cd spec/localhost

# 「sample_spec.rb」ディレクトリを編集
$ vim sample_spec.rb
```

- テストコード記述時に確認すること、注意点

テストコードを記述する際には、

    - リソースタイプ・・・テストの対象となる要素を指定。

    - マッチャー・・・リソースに対して期待する状態や振る舞いを表すこと
を組み合わせる。

```
例）
describe package('nginx') do
 it { should be installed }
end

例のテストコードにおけるリソースタイプとマッチャーはそれぞれ
リソースタイプ：package
マッチャー：should be_installed

このテストコードは
”Nginxはインストールされているか”をテストできる。

↓

コードの基本形
describe リソースタイプ('対象の何か(nginxやgitなど)') do
 it { マッチャー }
end
```

多様なマッチャーがある。serverspecサイトで確認可能。

- テスト実行
```
localhostディレクトリにて
$ rake spec
```

以下、テストコードの記述、検証結果

```
# ===追加コードニー=
# Nginxはインストールされているか
describe package( 'nginx') do
 it { should be installed }
end

# Nainxプロセスは実行中か
describe process ("nginx") do
 it { should be_running }
end

# 80番ポートをリスニングしているか
describe port (80) do
 it { should be listening } 
end

# 3306番ポートをリスニングしているか
describe port (3306) do
 it { should be_listening } 
end

# 指定されたポート（listen_portで指定された番号）に対して、HTTPリクエストを送信し、レスポンスのHTTPステータスコードが200であることを確認するテスト
describe command( curl http:/ /127.0.0.1:#{listen_port}/_plugin/head/ -o /dev/null
 its(:stdout) { should match /^200$/
end

# gitはインストールされているか
describe package ('git') do
 it { should be_installed } 
end
```

![テストコード](img/lecture11/serverspec%20テストコード%2011-1.png)

![検証結果](img/lecture11/serverspec%20検証結果%2011-2.png)





