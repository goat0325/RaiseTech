# RaiseTech学習事項

## 概要
RaiseTechのAWSコースにて、AWSを使用してインフラストラクチャを設計、構築、運用する実践的な経験を、各課題を通して学習してきました。

## 目的
学習の目的は、AWSサービス、インフラストラクチャの自動化、およびクラウドコンピューティングにおけるベストプラクティスに関する実践的な知識と経験を得る事です。

## 使用している主な技術
| 技術・ツール | 各サービス |
|--------------------|-----------------------|
| **AWS** | VPC/EC2/RDS/S3/IAM/ALB etc… |
| インフラストラクチャ | CloudFormation |
| 構成管理 | Severspec |
| CI/CDツール | CircleCI |
| バージョン管理 | GitHub |

## 動作環境
**ruby**
```
3.2.3
```
**Bundler**
```
2.3.14
```
**Rails**
```
7.1.3.2
```
**Node**
```
v17.9.1
```
**yarn**
```
1.22.19
```

## 学習記録の説明
RaiseTechにて、AWSを使用した実践的な経験を各課題を通して学習してきました。
各課題を.mdファイルにまとめ、mainブランチにマージする事によって記録しています。
下記に各課題内容を表記しています。

| 講座 | 概要 | 成果物 | 備考 |
|-------|----------|-----------|----|
| 課題1 | ・AWSアカウントの作成 <br> ・IAMの推奨設定（MFAで保護） <br> ・Cloud9にてHelloWorld出力 | - | RaiseTechのDiscord上にてスクリーンショットを提出 |
| 課題2 | ・バージョン管理システム「GitHub」を使った開発の流れ <br> ・Marrkdownでの記述 | - | - |
| 課題3 | ・Cloud9を使ったサンプルアプリケーションのデプロイ <br> ・相対Path(内部リンク)での記述 | [lecture03](lecture03.md) | Cloud9にて実施 |
| 課題4 | ・手動でインフラ環境を構築(VPC、EC2、RDS) <br> ・EC2 から RDS へ接続 | [lecture04](lecture04.md) | 以降VScodeにて実施 |
| 課題5 | ・EC2上にサンプルアプリケーションを手動でデプロイ（Puma、Unicorn、Nginxそれぞれで動作確認） <br> ・ALBとS3(IAMロール適用)を追加 <br> ・インフラ構成図作成 | [lecture05](lecture05.md) | サンプルアプリケーション内にアップロードした画像の保存にてS3を適用 |
| 課題6 | ・CloudTrail <br> ・CloudWatchアラームを利用したALBのアラーム設定 <br> ・AWS Pricing Calculatorを使用した利用料の見積もり <br> ・Cost Explorer Billing | [lecture06](lecture06.md) | - |
| 課題7 | ・AWS でのセキュリティ対策（脆弱性、認証情報の流出、人為的な過負荷） | [lecture07](lecture07.md) | 脆弱性の対策についてピックアップ | - |
| 課題8 | ・第5回課題のライブコーディング（組み込みサーバでの稼働まで） | - | - |
| 課題9 | 第5回課題のライブコーディング（Webサーバ・Railsアプリサーバ分離～最後まで） | - | - |
| 課題10 | ・CloudFormation | [lecture10](lecture10.md) | 第5回課題で作成した環境を構築 <br> EnvironmentNameを「test10」として構築 <br> VPC、EC2、RDS、ALB、S3に分解して作成 |
| 課題11 | ・インフラのコード化を支援するツール <br> ・Serverspecを利用したサーバーの環境構成テスト | [lecture11](lecture11.md) | 第5回課題にて作成した環境を利用してテスト実施 |
| 課題12 | ・CircleCIを使用したCI/CD | [lecture12](lecture12.md) | test10にて作成した「test10-vpc.yml」をコピーしたものを使用してテスト実行 |
| 課題13 | ・プロビジョニングツール（Ansible）を用いたインフラ環境構築の自動化 <br> ・CI/CDツールを使用したテスト実施 | - | 現在学習中 |
| 課題14 | 第13回課題のライブコーディング　前半 | - | - |
| 課題15 | 第13回課題のライブコーディング　後半 | - | - |
| 課題16 | 現場へ出ていくにあたって | - | - |

以上

