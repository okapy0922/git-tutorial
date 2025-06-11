# git-tutorial

Git＋GitHubの入門

## Clone
リモートリポジトリをローカルにクローンする（複製する）

```bash
git clone git@github.com:okada-t-www/git-tutorial.git
```


## Status
リポジトリ内の変更情報を確認するコマンド

```bash
git satus
```


## Stage
ステージングエリアとはリポジトリにコミットする前のバッファリングエリア
`README.md`ファイルをステージングエリアに追加するコマンド

```bash
git add README.md
```

## Commit
Gitリポジトリ内の変更をCommit（記録）するコマンド
```bash
git commit -m "コミットメッセージ"
```

## Push
ローカルリポジトリからリモートリポジトリに
変更をpush（同期）するコマンド

```bash
git push
```

## コマンド実行履歴
ターミナルで実行したコマンドの履歴を見る
「ｑ」を押して元に戻ります
```bash
git log
```

## プッシュテスト１

## プッシュテスト２
個人アカウントでプッシュしてしまっていたためつばさのアカウントに切り替えました
```bash
git config user.email "okada.t@example.com"
```
```bash
git config user.name "OkadaTakumi"
```
既存のコミットのユーザー情報を変更する
--amendオプションを使用してコミットを修正します
（直前のコミットを修正し、著者情報をリセットします。）
```bash
git commit --amend --reset-author
```
Ctrl + Xを押してからSave modified buffer?と聞かれるので
YまたはEnterキーを押し変更を保存

★今後気をつける
ローカルリポジトリの設定:

個人用のアカウントと会社用のアカウントを使い分けるために、
ローカルのリポジトリに対して適切なリモートリポジトリを関連付けます。

git remote addコマンドを使用して、リモートリポジトリを追加します。
```bash
git remote add <個人or会社> <個人or会社URL>
```
例：
```bash
git remote add personal https://github.com/okapy0922/pushtest.git
git remote add company https://github.com/okada-t-www/git-tutorial.git
```

## Branch ブランチ概要
![alt text](image.png)

## ブランチ表示

ローカルブランチの一覧を表示するコマンド

```bash
git branch
```

リモートブランチの一覧を表示するコマンド

```bash
git branch -r
git branch --remotes
```

すべてのブランチを表示するコマンド

```bash
git branch -a
git branch --all
```

## ブランチ操作

`feature`というbranchを新規作成するコマンド

```bash
git branch feature
```

`feature`ブランチを削除するコマンド

```bash
git branch -d feature
```

## Checkout(ブランチを切り替える)

`feature`ブランチに切り替えるコマンド

```bash
git checkout feature
```

`feature`ブランチを新規作成して`feature`ブランチにcheckoutするコマンド

```bash
git checkout -b feature
```

## git config --global(グローバル設定の確認と変更)

グローバル設定の確認
```bash
git config --global --local --list "
```
グローバル設定の変更
```bash
git config --global user.name "okada-t-www"
git config --global user.email "okada.t@example.com"
```

## Pull request概要
![alt text](image-1.png)

## Pull
リモートでの変更をローカルに反映させるコマンド

```bash
git pull
```

## .gitignoreについて
![alt text](image-2.png)

新しいファイルを作成「.gitigore」
ファイル名を記述
フォルダ名は後ろに「/」つける
![alt text](image-3.png)
=======
# Terraform_aws_cloudwatch_dashboard
## 主なtfファイルとコード内容
| ファイル名 | 説明 | 目的 |
|------------|------|------|
| `main.tf` | メイン設定ファイル | コアとなるインフラストラクチャリソース（Cloudwatchダッシュボードのメトリクス設定）を定義します |
| `variables.tf` | 変数定義 | Terraform設定全体で使用される入力変数を宣言します |
| `terraform.tfvars` | 変数割り当て | `variables.tf`で定義された変数に値を設定します |
| `outputs.tf` | 出力定義 | 設定適用後に出力すべき値を指定します |
| `providers.tf` | プロバイダー設定 | 必要なプロバイダー（AWSなど）とそのバージョンを設定します |
| `backend.tf` | バックエンド設定 | Terraformの状態をどこにどのように保存するか（S3バケットなど）を定義します |
| `data.tf` | データソース定義 | 既存のリソース情報を取得するためのデータソースを宣言します |
| `locals.tf` | ローカル値定義 | Terraform設定内で使用するローカル変数を定義します |
| `modules/` | モジュールディレクトリ | 共通のインフラストラクチャパターンのための再利用可能なTerraformモジュールを含みます |

## 主要なファイルの詳細

- **main.tf**: これは主要な設定ファイルでほとんどのリソース定義が含まれています。全体的なインフラストラクチャのセットアップを調整します。

- **variables.tf**: Terraform設定全体で使用できるすべての入力変数を宣言します。これにより、柔軟で再利用可能なコードが可能になります。

- **terraform.tfvars**: `variables.tf`で宣言された変数の実際の値を含みます。このファイルは通常gitignoreされ、環境ごとに異なります。

- **outputs.tf**: Terraformが設定を適用した後に出力すべき値を定義します。これは重要な情報を表示したり、Terraform設定間で値を渡したりするのに便利です。

- **providers.tf**: Terraform設定に必要なプロバイダーを指定し、その設定をセットアップします。

- **backend.tf**: 、Terraformが「状態ファイル」と呼ばれる重要な情報をどこに保存するかを指定するファイル。大規模なプロジェクトでも安全かつ効率的にインフラ管理が実現可能です。

- **data.tf**: Terraformによって作成されていない既存のリソースに関する情報を取得するために使用されます。

- **locals.tf**: Terraform設定全体で使用できるローカル変数を定義します。可読性向上に便利です。

- **modules/**: カスタムTerraformモジュールを含むディレクトリです。モジュールは、より良い組織化と再利用性のために、リソースグループをカプセル化するために使用されます。

## Cloudwatchダッシュボード作成に向けた汎用的なディレクトリ構造イメージ
```
project-root/
├── main.tf
├── variables.tf
├── terraform.tfvars
└── outputs.tf (オプション)
```
