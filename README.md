# CloudFormation Templates for Network and RDS

このリポジトリには、AWS CloudFormationを使用してネットワークとRDSを構築するためのテンプレートが含まれています。

## ファイル構成

- `network.yml`: ネットワーク構築用のCloudFormationテンプレート
- `rds.yml`: RDS構築用のCloudFormationテンプレート

## ネットワーク構成

```mermaid
```

## 使用方法

### 1. ネットワーク構築用テンプレートを実行

まず、`network.yml`を使用してネットワークリソースを作成します。

```bash
aws cloudformation create-stack --stack-name SingleRds-network-stack --template-body file://aws/cloudformation/network.yml
```

### 2. ネットワークスタックの作成が完了するのを待つ

ネットワークスタックの作成が完了するまで待ちます。以下のコマンドでスタックのステータスを確認できます。

スタックのステータスがCREATE_COMPLETEになったら次に進みます。

```bash
aws cloudformation describe-stacks --stack-name SingleRds-network-stack
```

### 3. RDS構築用テンプレートを実行

次に、rds.ymlを使用してRDSリソースを作成します。

- DBMasterUsernameとDBMasterUserPasswordの値は適宜変更してください。

```bash
aws cloudformation create-stack --stack-name SingleRds-rds-stack --template-body file://aws/cloudformation/rds.yml --parameters ParameterKey=DBMasterUsername,ParameterValue=[username] ParameterKey=DBMasterUserPassword,ParameterValue=[password]
```

### 4. RDSスタックの作成が完了するのを待つ

RDSスタックの作成が完了するまで待ちます。以下のコマンドでスタックのステータスを確認できます。

スタックのステータスがCREATE_COMPLETEになったら完了です。

```bash
aws cloudformation describe-stacks --stack-name SingleRds-rds-stack
```

### 注意事項

- DBMasterUserPasswordは強力なパスワードを使用してください。
- セキュリティグループの設定は適宜調整してください。
- テンプレート内のリソース名やパラメータは必要に応じて変更してください。

