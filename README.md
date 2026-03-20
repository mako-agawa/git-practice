# Git練習リポジトリ
Gitの基本操作を学ぶためのリポジトリです。

## 学習したコマンド一覧

### 基本操作

| コマンド | 意味 |
|---------|------|
| `git init` | リポジトリを新規作成 |
| `git status` | 現在の状態を確認 |
| `git add ファイル名` | ステージングエリアに追加 |
| `git add -A` | 全ての変更をまとめてステージング |
| `git commit -m "メッセージ"` | 変更を記録（コミット） |
| `git diff` | ステージング前の差分を表示 |
| `git log --oneline --graph` | 履歴をグラフで表示 |

### ブランチ操作

| コマンド | 意味 |
|---------|------|
| `git branch ブランチ名` | ブランチを作成 |
| `git checkout ブランチ名` | ブランチを切り替え |
| `git checkout -b ブランチ名` | 作成＋切り替えを同時に |
| `git branch` | ブランチ一覧を表示 |
| `git branch -d ブランチ名` | マージ済みブランチを削除 |
| `git merge ブランチ名` | ブランチを統合 |

### リモート操作（GitHub連携）

| コマンド | 意味 |
|---------|------|
| `git push` | ローカルの変更をGitHubに送信 |
| `git push -u origin ブランチ名` | 新しいブランチをGitHubに送信 |
| `git pull` | GitHubの最新をローカルに取り込む |
| `gh repo create` | GitHubにリポジトリを作成 |
| `gh pr create` | Pull Requestを作成 |
| `gh pr merge` | Pull Requestをマージ |

### 一時退避

| コマンド | 意味 |
|---------|------|
| `git stash` | 作業を一時退避 |
| `git stash list` | 退避一覧を表示 |
| `git stash pop` | 退避した作業を復元（リストから削除） |
| `git stash apply` | 復元（リストに残したまま） |

### 取り消し操作

| コマンド | 意味 |
|---------|------|
| `git reset --soft HEAD~1` | コミット取消（変更はステージングに残る） |
| `git reset HEAD~1` | コミット取消＋ステージング解除（ファイルは残る） |
| `git reset --hard HEAD~1` | コミット取消＋変更も完全に削除 ⚠️ |
| `git revert HEAD` | コミットを打ち消す新しいコミットを作成（安全） |
| `git reflog` | 全ての操作履歴を表示（最後の命綱） |

### エイリアス設定

| コマンド | 設定内容 |
|---------|---------|
| `git config --global alias.st status` | `git st` で status |
| `git config --global alias.co checkout` | `git co` で checkout |
| `git config --global alias.br branch` | `git br` で branch |
| `git config --global alias.cm "commit -m"` | `git cm` で commit -m |
| `git config --global alias.lg "log --oneline --graph"` | `git lg` でグラフ表示 |

## ポイントまとめ

### Gitの基本フロー
```
作業ディレクトリ → ステージング → リポジトリ → GitHub
    (編集)        (git add)    (git commit)  (git push)
```

### ブランチ運用サイクル
```
1. ブランチ作成 → 2. 作業・コミット → 3. push
       ↑                                  ↓
6. ブランチ削除 ← 5. pull ← 4. PR作成・マージ
```

### reset vs revert の使い分け
- **pushする前** → `git reset` （履歴を書き換える）
- **push済み** → `git revert` （打ち消しコミットを作る。安全）

### コンフリクト解消の手順
1. `git merge` でコンフリクト発生
2. 対象ファイルの `<<<<<<<` `=======` `>>>>>>>` を手動で編集
3. `git add` → `git commit` で解消完了

### 注意事項
- ターミナルでは**全角スペース**を使わない（コマンドが壊れる）
- `git reset --hard` は変更が完全に消えるので慎重に
- 困ったら `git reflog` で履歴を確認できる
