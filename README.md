# Github Project Test

業務効率化のため Github Actions を使用して Github Project や Issue の操作を行なってみる。

（以下自動生成です）

## 概要

このリポジトリは、GitHub Projectと連携したIssue管理を自動化するためのGitHub Actionsワークフローを提供します。Epicと子Issue（サブIssue）の関係を管理し、見積もり（Estimate）の集計を自動化することで、プロジェクト管理を効率化します。

## ワークフロー

### 1. Sub-Issue 管理 (`_add_label_subissues.yaml`)

新しいIssueが作成または編集されたときに自動実行されます。

**機能:**
- サブIssueを作成したタイミングで、「`subissue`」ラベルを自動付与
- 親Epic Issueに紐づいているラベル（「Epic」ラベルを除く）をサブIssueにも継承
- サブIssueを自動的にGithub Projectに追加

**トリガー:**
- Issue作成時
- Issue編集時

### 2. Epic Issue 見積もり集計 (`_aggregate_subissue_estimates.yaml`)

Epicに含まれるサブIssueの見積もり（Estimate）を集計して、Epicの見積もりフィールドに反映します。

**機能:**
- リポジトリ内のすべての「Epic」ラベルが付いたIssueを検索
- それぞれのEpicに含まれるサブIssueの「Estimate」値を集計
- 集計結果を「(Epic)Estimate」フィールドに設定
- オープン状態のサブIssueのみの合計を「(Epic)残Estimate」フィールドに設定

**トリガー:**
- 手動実行（workflow_dispatch）

## 必要な設定

### シークレット

以下のシークレットをリポジトリに設定する必要があります：

- `GITHUB_TOKEN`: 基本的なリポジトリアクセス用（GitHub Actionsで自動提供）
- `PROJECT_ACCESS_TOKEN`: GitHub Projectの操作に必要なパーソナルアクセストークン

### GitHub Project

以下のカスタムフィールドをプロジェクトに設定する必要があります：

- `Estimate`: 各Issueの見積もり値（数値フィールド）
- `(Epic)Estimate`: Epicの合計見積もり値（数値フィールド）
- `(Epic)残Estimate`: オープン状態のサブIssueの合計見積もり値（数値フィールド）

## 使用方法

1. Epicを作成し、「Epic」ラベルを付与
2. Epicの子となるサブIssueを作成（この時点で自動的にラベルが継承されます）
3. 各サブIssueの「Estimate」フィールドに見積もり値を設定
4. 「Epic Issue Estimation」ワークフローを手動実行して見積もりを集計

## 注意事項

- サブIssueを作成する際は、親Issueを正しく設定してください
- 「Epic Issue Estimation」ワークフローは定期的に実行することで、最新の見積もり状況を反映できます
