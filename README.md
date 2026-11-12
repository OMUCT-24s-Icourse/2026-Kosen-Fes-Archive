# Yukai Archive

2026年の学祭で展示した作品をまとめるWebサイトの叩き台です。
HTML/CSS/JavaScriptで構成し、GitHub Pagesで `docs/` を公開します。
Node.jsやビルドツールの準備は不要です。

## フォルダ構成

```text
Yukai-Archive/
├── README.md
└── docs/                       # GitHub Pagesの公開対象
    ├── .nojekyll                # Jekyllによる変換を行わない
    ├── index.html              # トップページ・展示一覧
    ├── 404.html                # 存在しないURLにアクセスした際のページ
    ├── assets/
    │   ├── css/
    │   │   └── style.css       # 全ページ共通のスタイル
    │   ├── js/
    │   │   └── script.js       # 全ページ共通の処理を追加する場所
    │   └── images/
    │       └── .gitkeep         # 展示写真などを置く場所
    └── exhibits/
        └── sample/
            └── index.html      # 複製して使う展示詳細のサンプル
```

## ローカルでの確認

`docs/index.html` をブラウザで直接開いて確認できます。
Python 3がある場合は、リポジトリのルートで次を実行しても確認できます。

```sh
python3 -m http.server 8000 --directory docs
```

ブラウザで <http://localhost:8000> を開きます。終了は `Ctrl+C` です。

Pythonの簡易サーバーは `404.html` を自動表示しません。
また、`404.html` のCSS・スクリプト・戻り先は公開先の `/Yukai-Archive/` を基準にしています。
404ページの確認は、公開後に存在しないURLを開くか、ローカルで同じURL構成を再現して行います。

## 展示を追加する

1. `docs/exhibits/sample/` をコピーし、展示ごとのフォルダを作ります。
   フォルダ名は `my-project` のような半角英数字とハイフンを推奨します。
2. コピー先の `index.html` のタイトル・概要・制作メンバー・本文を編集します。
   `TODO` コメントを目印に、サンプルの表記も実際の情報へ置き換えてください。
3. 写真は `docs/assets/images/my-project/` のように展示ごとに分けて置きます。
   詳細ページの画像枠を、例えば次のHTMLに置き換えます。

   ```html
   <img class="exhibit-image" src="../../assets/images/my-project/main.webp"
        alt="作品の見た目や展示の様子を説明する文章" width="1200" height="800">
   ```

   `width` と `height` は実際の画像サイズに合わせて変更してください。

4. `docs/index.html` のサンプルの `<li class="exhibit-card">` を複製し、
   展示名・概要・リンクを更新します。リンク例は `./exhibits/my-project/` です。
5. 実際の展示を登録したら、サンプルのカードと `docs/exhibits/sample/` を削除します。

通常のページのパスは相対パスにしてください。`/assets/...` のように `/` から始めると、
GitHub Pagesのリポジトリ配下のURLでリンク切れになることがあります。

`404.html` は表示されるURLの階層が一定でないため、例外として
`<base href="/Yukai-Archive/">` で公開先のパスを固定しています。
リポジトリ名を変更する場合はこの値も変更してください。
ユーザーサイトや独自ドメインでルートに公開する場合は `/` にします。

## 最初に編集する情報

- `docs/index.html`：サイト名、学祭名、開催日・会場、紹介文、展示一覧。
- 各展示の `index.html`：作品名、説明、写真、制作メンバー、関連リンク。
- `docs/assets/css/style.css`：色や余白などの共通デザイン。
- `docs/assets/js/script.js`：共通スクリプト。各ページから `defer` 付きで読み込み済みです。
  現時点では処理を追加するためのコメントだけを用意しています。
- `docs/404.html`：エラーメッセージ、トップページへの導線、公開先の基準パス。

現時点の展示や開催情報は、入力箇所を示すサンプルです。

## GitHub Pagesでの公開

ファイルをGitHubの `main` ブランチにpushした後、次の設定を行います。

1. リポジトリの **Settings → Pages** を開きます。
2. **Build and deployment → Source** で **Deploy from a branch** を選びます。
3. Branchを **main**、公開フォルダを **/docs** にして **Save** を押します。
4. デプロイ完了後、Pages設定画面に表示されるURLで確認します。

設定方法の詳細は [GitHub公式ドキュメント](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) を参照してください。
この叩き台では公開設定の変更やデプロイは行っていません。
