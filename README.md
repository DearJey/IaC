# Infrastructure as Code (IaC)

**Infrastructure as Code (IaC)** とは、CPU、メモリといったサーバのインフラ構築を、コードを用いて自動的に行うこと。

AWSで実現するにあたって、
* terraform
* cloudformation

が有名。

### IaCツール利用のメリット

インフラ構築のコード化により、自動で環境構築をしてくれるため、**手作業による人為的なミスを削減すること**が可能！ \
同じ環境を何台も作成しなければならない場合にも、自動構築してくれるため作業時間を短縮できる。

通常のソフトウェア開発と同じようにコードをバージョン管理することで、いつ修正したのかが明確となり、不具合の際などに第三者が検証しやすくなる。

## Terraform と CloudFormation

| - | terraform |	cloudformation |
| --- | --- | --- |
| 特徴 | OSSである。情報が多い。<br> バージョンが上がるごとにどんどん使いやすくなっている。機能も増えている。<br> コミュニティmoduleの存在 | AWSのサービスである。<br> サポートをしっかり受けられる |
| 実行方法 | 基本的にCLIで実行terraformコマンド<br>(terraform plan terraform applyだけ覚えておけばなんとかなる) | 基本的にGUIで実行。aws cloudformationコマンドもあるが、オプションが多いので学習コストが高い。 |
| セキュリティ | IAMの認証で実行する。<br> それぞれのローカル環境で実行することが基本のためセキュリティを意識する必要がある。 | AWSで閉じられるのでセキュリティで考えることが少ない |
| 初期設計 | 少しずつ始められる | 最初の設計が大事<br> stackの連携、管理する範囲をしっかり決めておく必要がある<br> 一度stack化すると削除⇒作成という流れを踏まなければいけないため |
| 設定言語 | 独自のスクリプト言語(.tf)を用いる | json、yaml形式を用いる |
| プラットフォーム | 複数プラットフォームに対応<br> AWSに縛られない | AWS専用サービス<br> 他のAWSサービスと連携がスムーズ |
| インポート | インポートが簡単。<br> terraform importコマンドを利用。 | import機能がある。 |
| CI/CD | CI/CD始めやすい。<br> JenkinsやCircleCI等外部ツールとも連携しやすい | Code4兄弟と連携させてCI/CD化できる。 |

## 参考

* Terraform連載 第1回：いまさら聞けない、IaCってなに？～Terraform、IaSQLの紹介～：https://www.ntt-tx.co.jp/column/iac/230815/

* 【AWS】terraformとCloudformationを比較してみた【IaC】：https://qiita.com/jucky330/items/9868dca2b13366a6d074
