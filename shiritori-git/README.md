# 🌱 Git練習：チームしりとり開発

このリポジトリは、Gitのブランチ運用・Pull Request・マージ・コンフリクト解消などの開発フローを体験するための「しりとり開発演習」です。

---

## 🧩 開発ルール

- 作業前に `git pull origin develop` を行ってください。
- 各自ブランチを切って作業（例：`feature/yamada-shiritori`）
- 1回の編集につき1単語を追加
- 編集が終わったら `develop` に対してPR（Pull Request）を作成
- レビューしたら `main` にマージします

---

## ✅ しりとりルール

- 最後の文字から始まる単語を追加する
- 単語は**名詞のみ**
- 「ん」で終わったらゲームオーバー
- 同じ単語の重複はNG
- Markdownの形式に従って記述すること

---

## 🌳 ブランチ構成

```
main      ← 本番ブランチ（完成した履歴のみ）
└── develop   ← 開発ブランチ（全Pull Requestをここにマージ）
    └── feature/あなたの名前 ← 各自の作業用ブランチ
```

---

## 🛠 開発手順（例）

1. リポジトリをクローン

   ```bash
   git clone git@github.com:lull-team-dev/practice-git.git
   cd practice-git/shiritori-git
   ```

2. `develop` を最新に

   ```bash
   git checkout develop
   git pull origin develop
   ```

3. 作業用ブランチを作成

   ```bash
   git checkout -b feature/yourname
   ```

4. `shiritori.md` に1行だけ単語を追加（※他の人が書いた最後の行からつなげる）

5. 変更をコミットしてプッシュ

   ```bash
   git add shiritori.md
   git commit -m "Add: しりとり単語「ごりら」"
   git push origin feature/yourname
   ```

6. GitHub上で Pull Request を作成（`base: develop`）

7. レビューを受けてマージ（or 誰かがマージ）

8. 他の人が先にマージしていたら：

   ```bash
   git pull --rebase origin develop
   ```

---

## ⚠️ 注意点

- `main` ブランチには**直接コミット・マージ禁止**（保護ブランチ）
- `develop` が常に最新になるように `pull` を忘れずに
- Pull Request の際は、**他の人のしりとりルールもチェックしてから**マージしましょう
- コンフリクトが発生した場合は、**しりとりの順番を守りながら手動で解決**してください

---

## 📎 ファイル構成

```
shiritori.md    # しりとりの本体（1行1単語）
README.md        # この説明ファイル
```

---

## 👥 チーム練習で身につくこと

- `git pull`, `commit`, `push`, `pull request`
- コンフリクトの原因と解消手順
- ブランチの使い分けとレビューの流れ
- GitHub Flow / Git-flow の考え方

---

楽しく、でも本番さながらの練習を一緒に進めましょう ✊✨

---

# 🧩 コンフリクト解消マニュアル（しりとり開発用）

## ✅ コンフリクトとは？

複数人が同じファイルの同じ場所（今回は `shiritori.md` の末尾）を同時に編集して、
Gitがどちらを採用すべきか判断できず、**手動で選択が必要な状態**のことです。

---

## 🔥 よくある例

- Aさん：`ごりら` を追加
- Bさん：同時に `らっぱ` を追加

両方が `develop` にPull Request → マージしようとすると、**コンフリクトが発生**します。

---

## 🪛 解決手順（VSCodeを使用する場合）

### 🔹 1. 最新のdevelopを取り込む

```bash
git pull --rebase origin develop
```

> 🔺 このタイミングで「CONFLICT」と表示されたら、マージ競合が起きています。

---

### 🔹 2. コンフリクトしたファイル（例：`shiritori.md`）を開く

内容はこのようになっています：

```txt
りんご
ごりら
<<<<<<< HEAD
らっぱ
=======
らいおん
>>>>>>> origin/develop
```

---

### 🔹 3. 正しいしりとりの流れを確認して、1つだけ残す or 合成する

#### ❌ 悪い例（両方残してる）

```txt
ごりら
らっぱ
らいおん
```

→ しりとりが2重に進んでしまっており、流れが壊れます。

#### ✅ 良い例（後勝ち or手動で合意）

```txt
ごりら
らっぱ
```

または

```txt
ごりら
らいおん
```

➡ コンフリクト部分を修正後、**コンフリクトマーカー（`<<<<<<<`など）を全て削除**してください。

---

### 🔹 4. 解消できたらステージングとコミット

```bash
git add shiritori.md
git rebase --continue
```

または：

```bash
git commit -m "コンフリクト解消: ごりら vs らっぱ"
```

---

## 🔁 よく使うGitコマンドまとめ

| コマンド | 内容 |
|----------|------|
| `git status` | コンフリクト中のファイルを確認 |
| `git diff` | 差分確認 |
| `git add <file>` | 解決後のファイルをステージ |
| `git rebase --continue` | rebaseを続行（rebase中のみ） |
| `git merge --abort` | マージを中止（マージ中のみ） |

---

## 💡 チーム内の相談ポイント

- どちらの単語を採用するか迷ったら、**Slackや対面で相談**
- `らっぱ` と `らいおん` どちらがいいか → 順番をずらして両方入れる案もOK
- **意味が通るか？ しりとりとしてつながるか？** も判断基準に！

---

## ✅ 最後に：一人で悩まず、チームで解消！

Gitのコンフリクトは怖くありません！  
**しりとりを通じてチームで練習するのが目的**なので、  
「誰かと一緒に解決する」ことも大事な経験です💪

