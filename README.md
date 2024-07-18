# ①課題番号-プロダクト名

じゃんけんアプリ

## ②課題内容（どんな作品か）

- 手を選んでpcと戦うじゃんけんゲームを作成しました。

## ③DEMO
- さくらサーバ
    -  https://tech-yusuke.sakura.ne.jp/challenge-project-github-handson/
- AWS S3 + CloudFront
    - https://d2i5073jzaeclp.cloudfront.net/

## ④作ったアプリケーション用のIDまたはPasswordがある場合
- 無し
<!-- - ID: 〇〇〇〇〇〇〇〇
- PW: 〇〇〇〇〇〇〇〇 -->

## ⑤工夫した点・こだわった点
- javascriptのコードについて、5行で規定の要件を達成できるように書き方を工夫した
  ```
  $("ul li").on("click", function() {
  const computerHand = Math.floor(Math.random() * 3); // コンピュータの手をランダムに決定
  $("#pc_hands").html( ["グー", "チョキ", "パー"][computerHand]);
  $("#judgment").html( ["引き分け", "負け", "勝ち"][($(this).index() - computerHand + 3) % 3]);
  });
- AWSのS3とCloudFrontを使って外部にページを公開できるようにした
    - +CloudFormationを使ってインフラの設定をIaCで管理する方法でデプロイを行った
- WebページにオブザバビリティプラットフォームのNewRelicを導入し、処理遅延箇所のモニタリングやエラー検知等をできるようにした
- githubを使いながら機密情報を安全な方法で管理できるようにした
    - NewRelic連携にあたって、コードの中にlicensekeyを入れる必要があると考えたため
        - githubの公開リポジトリでコードを管理しつつkey部分をファイルとして分離し、git-cryptを使って暗号化した状態で公開することで情報漏洩を防ぐ仕組みを構築した。

## ⑥難しかった点・次回トライしたいこと(又は機能)
- 難しかった点
    - licensekeyを安全にgit上で管理できるようにするのが大変でした。
    - さくらサーバについてはうまくファイルのアクセス制御ができなかったので質問させていただいています。（ファイルのアクセス制限をすると、ブラウザから確認できなくなってうまく機能しない、、）
- 次回トライしたいこと
    - 今後も出来上がった機能をさくらサーバでのデプロイと、AWSの各機能を連携させたデプロイを両方行っていきたい。その際はCloudFormationでリソース管理できるようにしたい。
    - AWSのデプロイについて、githubと連携させた形でサイトの内容やインフラ設定を変更できるようにしたい。
    - NewRelicでどのような情報が確認できるかについて詳しくみていきたい。
        - さくらサーバとCloudFrontの違いについても確認していきたい。

## ⑦質問・疑問・感想、シェアしたいこと等なんでも

- [質問]
    - 機密情報を含むコードをgitで管理して、さくらサーバでデプロイする場合に安全に機密情報を管理する他のおすすめの方法があれば教えていただきたいです。特に、さくらサーバ上では特定のファイルを非公開にするとブラウザに適切に値を読み込むことができなくなってしまったので、うまく情報管理する方法を知りたいです。
- [感想]
    - さくらサーバでのデプロイに加えて、NewRelicの導入方法やgit-cryptoを使った機密情報の管理方法を学びながら実践できてよかったです。
    - NewRelicののlicensekeyは結局漏れても大丈夫（ベストプラクティスに沿っている）ということを、どのようなリスクがあるか含めNewRelicのエンジニアの方と直接ディスカッションしながら学ぶことができて知見が深まりました。
- [参考記事]
  - CloudFormationを使ったwebサイトのデプロイ
    - https://dev.classmethod.jp/articles/cfn-s3-webhosting-cloudfront/
  - newrelic公式無料ハンズオン
    - https://app.path.progate.com/tasks/muzHlTIVNZkSxom_eL_be/preview
  - git-cryptの初期設定
    - https://qiita.com/batch9703/items/f6959ba51bb9bb32ef93
  - NewRelicのlicensekeyに関するonlineコミュニティ上のコメント
    - https://forum.newrelic.com/s/hubtopic/aAX8W0000008Zh6WAE/newrelic-license-for-spa-is-openexposed
  - さくらインターネットで一部のフォルダを非公開設定にする方法
    - https://help.sakura.ad.jp/rs/2196/#03
  - git-cryptを使った解凍コマンド
    - ```
      git-crypt unlock
