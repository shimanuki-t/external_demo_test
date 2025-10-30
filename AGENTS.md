# ファイル整理方針

## 前提

本ディレクトリ配下に下記フォルダがあるか確認してください。

無ければ、本ディレクトリ配下に作成すること。

### 必要なフォルダ一覧

- `0.Reference`
- `1.Background_goal`
- `2.Consider_plan_cost_risk`
- `3.Final_plan`

---

## 整理

ファイルの内容を見て、その内容が上記フォルダのどのフォルダに保存するのが相応か判断し、配下に保存すること。  
(README.mdはリポジトリのルートディレクトリに置き、README.mdから参照しているファイルのパスは適宜変更すること。)

### フォルダの用途

- **0.Reference**: 参考資料や外部ドキュメント
- **1.Background_goal**: 背景情報やプロジェクトの目標
- **2.Consider_plan_cost_risk**: 検討事項、考慮すべき点、計画、コスト、リスク分析
- **3.Final_plan**: 最終的な計画書や成果物

---

## GitHub PRコマンド実行時、Gitコミットメッセージ追加時の注意点

Windows環境でGitHub CLIを使用する際、日本語の文字化けを防ぐために以下の方法を使用してください。

### タイトルの文字化け対策

エンコーディングを明示的にUTF-8に指定してファイルから読み込みます。

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8; $title = Get-Content pr_title.txt -Encoding UTF8 -Raw; gh pr edit 4 --title $title.Trim()
```

**ポイント:**
- `[Console]::OutputEncoding`でコンソールの出力エンコーディングをUTF-8に設定
- `Get-Content`で`-Encoding UTF8`を指定してファイルを読み込み
- `-Raw`でファイル内容を単一の文字列として取得
- `.Trim()`で前後の空白や改行を削除

### 本文の文字化け対策

本文は`--body-file`オプションを使用して外部ファイルから読み込みます。

```bash
gh pr create --base main --head feature/update-github-issue-rule --title "feat: GitHub Issue作成ルールを実際のプロジェクト設定で更新" --body-file pr_body.txt
```

**ポイント:**
- `--body`オプションではなく`--body-file`オプションを使用
- GitHub CLIが自動的に適切なエンコーディングでファイルを読み込む
- 複数行の本文を扱う場合にも有効

### 推奨事項

1. PRのタイトルや本文に日本語を含む場合は、必ず外部ファイル経由で指定する
2. ファイルはUTF-8エンコーディングで保存する
3. PowerShellの場合は`[Console]::OutputEncoding`の設定も併用する

## SVGファイルの読み込みについての注意
SVGファイルを読み込むとき、read_fileツールは絶対に利用しないこと。  
(現段階だとサポート対象じゃないと読み込みエラーが起きるから。)
