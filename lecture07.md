# 第7回課題

## 課題内容
1. 課題の感想や疑問を報告
    - 今作っている環境はどんな攻撃に対して「脆弱」か
    - どのような対策が取れそうか

1. 課題の感想や疑問

- どんな攻撃に対して「脆弱」か

    - SQLインジェクション
    ```
    WebサイトやWebアプリケーションの脆弱性につけこみ「SQL（データベースを操作するための言語）」を用いて、不正なSQL文を「データベース」に送り、個人情報の窃取やデータ改ざんなどを行う攻撃手法
    ```

- どのような対策が取れそうか

    - Dependabot
    ```
    モジュール、ライブラリの更新を知らせてくれることによって、細めにアップデートをする
    ```

    - WAF
    ```
    OWASP top 10にも記載のある脆弱性における問題点をルールに組み込み防ぐ
    ```

    - Amazon Inspector
    ```
    CVSS（JVN）に基づいたOS、ミドルウェアの脆弱性をスキャン。起こっている問題の危険度を確認、対処を検討できる
    ```

    - IAMの権限設定
    ```
    「最小限の法則」に則り、不要な権限は最終的に拒否しておく
    ```

## 感想や疑問
講座やOWASP top 10などのサイトを見てみると、サイトを動かし続けるだけでも、多くの問題が起こる可能性があり、一つの問題に対して、複数の対処方法を検討する必要があることを確認できました。ただ、どこまで対処を検討するべきなのか、考え出すとキリがないようにも感じたので、チーム内での方向性のすり合わせは必要だと感じました。