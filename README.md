# CloudFormationによるIAMユーザー作成

このリポジトリは、AWSで一時的なIAMユーザーを作成するためのCloudFormationテンプレート（`iamuser.yaml`）を含んでいます。

## 概要

このテンプレートは、以下のタスクを自動化します。

*   新しいIAMユーザーを作成します。
*   ユーザーに一時的なパスワードを割り当てます（初回ログイン時にパスワードの変更が要求されます）。
*   指定された既存のIAMグループにユーザーを追加します。

## 前提条件

*   AWSアカウントを持っていること。
*   AWS CLIがインストールおよび設定済みであること。
*   ユーザーを追加するためのIAMグループがすでに存在していること。

## 使用方法

このスタックは、AWSマネジメントコンソールまたはAWS CLIを使用してデプロイできます。

**AWS CLIを使用する場合:**

```bash
aws cloudformation create-stack \
  --stack-name my-iam-user-stack \
  --template-body file://iamuser.yaml \
  --parameters ParameterKey=TestGroup,ParameterValue=あなたのグループ名 \
               ParameterKey=Password,ParameterValue=安全なパスワード
```

`あなたのグループ名` と `安全なパスワード` は、任意の値に置き換えてください。

## パラメータ

*   `TestGroup` (String): ユーザーを追加する既存のIAMグループ名。デフォルト: `CloudOps`
*   `Password` (String): 新規ユーザーの初期パスワード。ユーザーは初回ログイン時にこのパスワードを変更する必要があります。デフォルト: `password`。**このデフォルト値は必ず変更することを強くお勧めします。**

## クリーンアップ

このスタックによって作成されたリソースを削除するには、CloudFormationスタックを削除してください。

```bash
aws cloudformation delete-stack --stack-name my-iam-user-stack
```

これにより、スタックによって作成されたIAMユーザーが削除されます。
