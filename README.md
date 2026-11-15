# 割り勘・精算計算ツール 公開パッケージ

GitHub Pages にそのままアップロードして公開するための一式です。すべて単独で動作する静的ファイルで、外部リソース（CDN・外部フォント等）は使っていません。

## ファイル構成

| ファイル | 内容 |
|---|---|
| `index.html` | ツール本体（クイック割り勘＋立て替え精算） |
| `guide.html` | 解説ページ（端数の扱い方・立て替え精算の具体例） |
| `sitemap.xml` | 検索エンジン向けサイトマップ |
| `robots.txt` | クローラー向け設定（sitemap の場所を通知） |
| `README.md` | このファイル |

## 公開手順（GitHub Pages）

1. GitHub にログインし、新しいリポジトリを作成する（名前は `warikan` を推奨。Public にする）
2. このフォルダのファイルをすべてリポジトリ直下にアップロードする（`Add file` → `Upload files`）
3. リポジトリの `Settings` → `Pages` を開く
4. `Build and deployment` の Source で `Deploy from a branch` を選び、Branch は `main` / `(root)` にして `Save`
5. 数分待つと `https://mini-tools-lab.github.io/warikan/` で公開される（`mini-tools-lab` は自分の GitHub ユーザー名）

### URL のプレースホルダ差し替え

ファイル内の URL はプレースホルダ `https://mini-tools-lab.github.io/warikan/` で書いてあります。そのままでもページの動作には支障ありませんが、公開したら次の3ファイル内の `mini-tools-lab` を自分のユーザー名に置き換えておくと、検索エンジンへの登録（Google Search Console への sitemap 送信など）が正しく行えます。

- `index.html` の canonical / og:url
- `guide.html` の canonical / og:url
- `sitemap.xml` と `robots.txt` の URL

## 後から独自ドメインを設定するときの注意

- GitHub 側： `Settings` → `Pages` → `Custom domain` にドメインを入力すると、リポジトリに `CNAME` ファイルが自動で作られる（このファイルは消さないこと）
- DNS 側： サブドメイン（例 `warikan.example.com`）なら `CNAME` レコードで `mini-tools-lab.github.io` を向ける。ルートドメインの場合は GitHub 公式ドキュメントの A / ALIAS レコード設定に従う
- HTTPS： DNS が反映されると Let's Encrypt の証明書が自動発行される。`Enforce HTTPS` にチェックが入るようになってから有効化する（反映まで最大で1日程度かかることがある）
- URL の差し替え： ドメインを付けたら、上記3ファイル内の URL（canonical・og:url・sitemap・robots）を **新しいドメインの URL にすべて差し替える**。古い `github.io` の URL が残っていると、検索エンジンが旧URLを正として扱うことがある
- Search Console 等に旧 URL で登録していた場合は、新ドメインで登録し直す
