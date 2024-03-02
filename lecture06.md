# 第6回課題

## 課題内容
1. AWSを利用した日の記録を、Cloud Trailのイベント履歴から選択（イベント名、含まれている内容を３つピックアップ）

2. Cloud watchアラームを利用したALBのアラーム設定、メール通知まで
    1. Unhealthy時
    2. OK時（Healty時）

3. AWS利用時の見積もり
    1. 見積もりの共有
    2. 請求情報より、先月のEC2の利用料金


## 1.AWSを利用した日の記録を、Cloud Trailのイベント履歴から選択（イベント名、含まれている内容を３つピックアップ）

- Cloud Trail作成
![loud Trail作成画面](img/lecture06/01%20Cloud%20Trail1.png)

- イベント履歴
    - イベント名：Update Trail = Cloud Trail設定の更新
    - 内容1：userIdentity = リクエストを実行したユーザー情報
    - 内容2：eventTime = イベントを実行した時間
    - 内容3：sourceIPAddress = リクエストの送信元のIPアドレス。49.109.108.225



![cloud trailイベント画面1](img/lecture06/02%20Cloud%20Trail2.png)
![cloud trailイベント画面2](img/lecture06/03%20Cloud%20Trail3.png)
![cloud trailイベント画面3](img/lecture06/04%20Cloud%20Trail4.png)
![cloud trailイベント画面4](img/lecture06/05%20Cloud%20Trail5.png)


## 2. Cloud watchアラームを利用したALBのアラーム設定、メール通知まで

- Cloudwatchアラーム作成

1. Unhealthy時にアラーム
    - AZ:ap-northeast-1a
    - メトリクス名：UnHealthyHostCount
    - アラーム状態トリガー：アラーム状態
    - アラーム名：alarm_loadbalancer_unhealthy_count　　にてアラーム作成

![Unhealthy 画面1](img/lecture06/06%20ALB%20unhealthy1.png)
![Unhealthy 画面2](img/lecture06/07%20ALB%20unhealthy2.png)
![Unhealthy 画面3](img/lecture06/08%20ALB%20unhealthy3.png)
![Unhealthy メール](img/lecture06/09%20ALB%20unhealthy%20mail.png)


2. OK（Healty時）にアラーム
    - AZ:ap-northeast-1a
    - メトリクス名：UnHealthyHostCount
    - アラーム状態トリガー：OK
    - アラーム名：alarm_loadbalancer_unhealthy_count_OK　　にてアラーム作成

![healthy 画面1](img/lecture06/10%20ALB%20healthy%20OK1.png)
![healthy 画面2](img/lecture06/11%20ALB%20healthy%20OK2.png)
![healthy 画面3](img/lecture06/12%20ALB%20healthy%20OK3.png)
![healthy メール](img/lecture06/13%2010%20ALB%20healthy%20OK%20mail.png)


## 3. AWS利用時の見積もり

1. 見積もりの共有
    - [見積もり](https://calculator.aws/#/estimate?id=3b30e4531fff07535a532554067aa48aebf57cca)

2. 請求情報より、先月のEC2の利用料金
![先月のEC2見積もり](img/lecture06/14%20EC2%20cost.png)

-free tier確認　無料利用枠で収まっている