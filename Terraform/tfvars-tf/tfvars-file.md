# tfvarsファイルとは?

宣言された変数の値を設定するファイル。

## tfvarsファイルが解決する3つの課題

1. **環境分離の実現**： \
   * 同じTerraformコードを異なる環境で再利用可能
   * 環境固有の設定値を明確に分離
   * 設定値の一元管理による保守性向上

2. **セキュリティの向上**： \
   * 機密情報（APIキー、パスワードなど）をコードから分離
   * アクセス制御の適用が容易
   * バージョン管理からの除外が可能

3. **チーム開発の効率化**： \
   * 設定値の標準化
   * レビュープロセスの簡素化
   * 変更履歴の追跡が容易

## tfvarsファイルの基本的な使い方・設定方法

```
# 基本的な変数定義
region = "ap-northeast-1"
instance_type = "t2.micro"

# リスト型の変数
availability_zones = ["ap-northeast-1a", "ap-northeast-1c"]

# マップ型の変数
tags = {
  Environment = "production"
  Project     = "example"
  Owner       = "team-infra"
}
```
命名規則のベストプラクティス：
* デフォルト設定ファイル: `terraform.tfvars`
* 環境別設定ファイル: `環境名.tfvars（例：dev.tfvars, prod.tfvars）`
* 機密情報用ファイル: `secrets.tfvars`



---

## 参考

* 【保存版】terraform tfvarsの基礎から実践まで完全解説！7つの活用テクニック：https://dexall.co.jp/articles/?p=2337#i-0
