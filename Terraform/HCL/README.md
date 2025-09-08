# HCL（HashiCorp Configuration Language）

**[HCL（HashiCorp Configuration Language）](https://developer.hashicorp.com/terraform/language/syntax/configuration)** は、HashiCorp社が開発した宣言型の設定言語。 \
主にインフラ構成管理ツールのTerraformやConsul、Vaultなどで使われている。

## 主な特徴

* 人間に優しい記法（JSONライクだが、より直感的）
* 宣言型：望む状態を記述する
* データ構造や構成管理に強い
* JSONとの互換性（HCL→JSON変換が可能）

## HCLのメリット・デメリット

### メリット

* **可読性が高い**： \
  人間が読み書きしやすい構造。設定ファイルの管理・レビューが楽。

* **宣言型で直感的**： \
  望む状態を記述するだけで、ツールが詳細な手順を自動化。

* **拡張性と柔軟性**： \
  モジュール化や再利用、条件分岐、変数などもサポート。

* **JSON互換**： \
  HCLで書いた設定はJSONにも変換可能。既存ツールとの連携も容易。

* **多くのHashiCorp製品で利用可能**： \
  Terraformだけでなく、ConsulやVaultなどでも活躍。

### デメリット

* **HashiCorp製品以外での採用が少ない**： \
  他社ツールではあまり使われていない。

* **学習コスト**： \
  JSONやYAMLに慣れている人には独自の記法がやや新鮮。

* **ツール間の微妙な仕様差**：

製品ごとにHCLの拡張や制限があり、細かい違いに注意が必要。

## 文法・構造

HCLはブロック、属性、値で構成される。

* AWS EC2インスタンスを定義するサンプル
```
resource "aws_instance" "example" {
  ami           = "ami-123456"           # AMI ID（文字列）
  instance_type = "t2.micro"             # インスタンスタイプ（文字列）
  count         = 3                      # インスタンス数（数値）
  enabled       = true                   # 有効化フラグ（ブール値）

  tags = {                               # タグ（マップ型）
    Name = "Example"
    Env  = "Dev"
  }

  names = ["web", "db", "cache"]         # インスタンス名リスト（リスト型）
}
```

1. **ブロック（Block）**
   * 構成要素をグループ化する単位
   * 例：`resource`、`variable*など
```
resource "aws_instance" "example" {
  # 属性と値を書く
}
```

2. **属性（Attribute）**
   * ブロック内で設定するパラメータ
   * `key = value` の形式
```
instance_type = "t2.micro"
```

3. **値（Value）**
文字列、数値、ブール値、リスト、マップなど
```
ami           = "ami-123456"
count         = 3
enabled       = true
tags          = { Name = "Example" }
names         = ["web", "db", "cache"]
```

* **データ型**
  * 文字列："example"
  * 数値：42
  * ブール値：true / false
  * リスト：["a", "b", "c"]
  * マップ：{ key1 = "value1", key2 = "value2" }
 
* **コメント**
  * `#` または `//` で記述可能
```
# これはコメント
// これもコメント
```