# terraform.tfvarsとvariables.tf

## 1.基本的な役割

### 1.1. variables.tf

* 変数の宣言を行うファイル。
* 変数の型定義、説明、デフォルト値を設定。
* インフラストラクチャのコードで使用する変数の「型」や「構造」を定義する。

例えば、VPCのCIDRブロックを定義する場合、variables.tfでは以下のように変数を宣言する。： \
※ 全てのパラメータは必須ではない。
* variables.tf
```sh
variable "vpc_cidr" {
  type        = string
  description = "CIDR block for the VPC"
  default     = "10.0.0.0/16"
}
```

### 1.2. terraform.tfvars

* 宣言された変数の値を設定するファイル。
* `variables.tf`で宣言された変数に具体的な値を割り当てる。
* 環境ごとに異なる設定値を管理するのに適している。

例えば、terraform.tfvarsでは以下のように値を設定する。：
* terraform.tfvars
```sh
vpc_cidr = "20.0.0.0/16"  # 本番環境用のVPC CIDR
```

## 2. デフォルト値の挙動

* **優先順位**：
  1. `terraform.tfvars`で設定された値が最も優先される。
  2. 次に環境変数（TF_VAR_変数名）が優先される。
  3. 最後にvariables.tfのdefault値が使用される。

* **デフォルト値の使用条件**：
  1. `terraform.tfvars`や環境変数で値が設定されていない場合のみ、`variables.tf`のdefault値が使用される。
  2. default値が設定されておらず、他の方法でも値が提供されていない場合、Terraformは実行時に値の入力を求められる。

#### 実例：

* `variables.tf`でproject_idのデフォルト値が"ax00000"と設定されている。
* `terraform.tfvars`では`project_id = "dev"`と設定されている。 \
  → \
  **実際に適用される値は"dev"になる。**


## 3. 変数定義の注意点

### 3.1. 同じ変数に対する複数の値の定義

* `terraform.tfvars`内で同じ変数に複数回値を割り当てた場合、**最後の定義が優先される**： \
  例えば、以下のようにaws_regionが2回定義されている場合：
```
# terraform.tfvars
aws_region = "us-west-1"
# 中略
aws_region = "ap-northeast-1" #優先される
```

### 3.2. 変数が宣言されていない場合

* `variables.tf`**で宣言されていない変数をterraform.tfvarsで定義しても、その変数は使用されない。**
* Terraformはエラーを出し、未定義の変数が指定されていることを警告する。

---

## 参考

* Terraformにおけるterraform.tfvarsとvariables.tfの関係性と挙動を理解する：https://zenn.dev/delta_tsuruta/articles/68422ed5761500

* 【保存版】terraform tfvarsの基礎から実践まで完全解説！7つの活用テクニック：https://dexall.co.jp/articles/?p=2337
