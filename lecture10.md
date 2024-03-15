# 第10回課題

## 課題内容
1. CloudFormation を利用して、現在までに終った環境をコード化してみる
   - コード化ができたら実行してみて、環境が自動で作られることを確認

## 1. CloudFormation を利用して、現在までに終った環境をコード化してみる

- EnvironmentNameを「test10」　として、下記構成図のように作成

![第5回課題のインフラ構成図](img/lecture05/21-architecture.png)

### スタック作成
スタックを各リソースごとに作成
1. VPC、サブネット、ルートテーブル、インターネットゲートウェイ
2. EC2、付随するセキュリティグループ
3. RDS、付随するセキュリティグループ
4. ALB、ターゲットグループ、付随するセキュリティグループ
5. S3、IAMのポリシー、ロール


###
1. VPC、サブネット、ルートテーブル、インターネットゲートウェイ

以下、CloudFormationで作成したリソースを記載
```
・VPC作成
        - VPC

・サブネット作成
    パブリックサブネット×２
        - PublicSubnet01
        - PublicSubnet02

    プライベートサブネット×２
        - PrivateSubnet01
        - PrivateSubnet02

・ルートテーブル作成
    パブリックサブネット用
        - PublicRouteTabl

    プライベートサブネット用
        - PrivateRouteTable

・作成したサブネットを、それぞれのルートテーブルへ割り振り
    パブリックサブネット×２　→ パブリックサブネット用のルートテーブルへ
        - PublicSubnet01RouteTableAssociation
        - PublicSubnet02RouteTableAssociation

    プライベートサブネット×２　→　プライベートサブネット用のルートテーブルへ
        - PrivateSubnet01RouteTableAssociation
        - PrivateSubnet02RouteTableAssociation

・InternetGateway作成
        - InternetGateway

    VPCにアタッチ
        - InternetGatewayAttachment

    パブリックルートテーブルとアタッチ
        - InternetGatewayToRouteTable
```
- VPC作成画面
![VPC画面](img/lecture10/lecture10-01%20vpc.png)

- パブリックサブネットリソースマップ
![パブリックサブネットリソースマップ](img/lecture10/lecture10-02%20IGW-PublicSubnetリソースマップ.png)

- プライベートサブネットリソースマップ
![プライベートサブネットリソースマップ](img/lecture10/lecture10-03%20PrivateSubnetリソースマップ.png)

2. EC2、付随するセキュリティグループ

以下、CloudFormationで作成したリソースを記載
```
・EC2インスタンス作成
        - EC2
    
・セキュリティグループ作成
        - EC2SecurityGroup
```
- EC2作成画面
![EC2作成画面](img/lecture10/lecture10-04%20ec2.png)

- EC2セキュリティグループ
![EC2セキュリティグループ](img/lecture10/lecture10-05%20ec2-sg.png)

- SSH接続確認画面
![SSH接続確認画面](img/lecture10/lecture10-06%20SSH接続確認.png)

3. RDS、付随するセキュリティグループ

以下、CloudFormationで作成したリソースを記載
```
・RDS作成
        - RDSInstance
    
・RDSサブネットグループを定義
        - RDSSubnetGroup

・RDSのセキュリティグループ作成
        - RDSSecurityGroup
```

- RDS作成画面
![RDS作成画面](img/lecture10/lecture10-07%20RDS.png)

- RDSセキュリティグループ
![RDSセキュリティグループ](img/lecture10/lecture10-08%20RDS-sg.png)

- RDSサブネットグループ
![RDSサブネットグループ](img/lecture10/lecture10-09%20RDSサブネットグループ.png)

4. ALB、ターゲットグループ、付随するセキュリティグループ

以下、CloudFormationで作成したリソースを記載
```
・ALB作成
        - ALB

・ALBのセキュリティグループ作成
        - ALBSecurityGroup
    
・ALBのリスナー作成
        - ListenerHTTP

・ターゲットグループ作成
        - ALBTargetGroup
```
- ALB作成画面
![ALB作成画面](img/lecture10/lecture10-10%20ALB.png)

- ALBセキュリティグループ
![ALBセキュリティグループ](img/lecture10/lecture10-11%20ALB-sg.png)

- ターゲットグループ
![ターゲットグループ](img/lecture10/lecture10-12%20TargetGroup.png)

5. S3、IAMのポリシー、ロール

以下、CloudFormationで作成したリソースを記載
```
・S3バケット作成
        - S3Bucket

・EC2へ、「AmazonS3FullAccess」ポリシーを許可するロールをアタッチする
    アクセスロール
        - S3AccessRole

    アクセスポリシー
        - S3AccessPolicies
    
    EC2インスタンスとロールを紐付けるために、IAMインスタンスプロファイルを記述
        - S3AccessInstanceProfile
    
●S3AccessInstanceProfile作成後、EC2用のスタックのEC2内「IamInstanceProfile」にインポート
```

- S3作成画面
![S3作成画面](img/lecture10/lecture10-13%20S3.png)

- IAMロール確認
![IAMロール確認](img/lecture10/lecture10-15%20IAMロール.png)

- AmazonFullAccessポリシーが許可されていることを確認
![許可ポリシー](img/lecture10/levture10-14%20許可ポリシー.png)