# 2.hogehoge.co.jp

株式会社hogehoge の「懐かしのホームページ」風サイトです。
90年代〜2000年代初頭のウェブサイトの雰囲気を再現した、単一 HTML ファイルで完結するページです。

公開URL: https://2.hogehoge.co.jp

## クレジット

このサイトは **[ダサウェブ★メーカー](https://amix-design.com/asoboad/tools/d-dasaweb/)** で作成しました。

- **制作ツール**: ダサウェブ★メーカー — 「懐かしいホームページを、1枚のHTMLで」
- **ツール制作**: トミナガハルキ さん（[ASOBOAD](https://amix-design.com/asoboad/) / [@asobodesign](https://x.com/asobodesign)）
- **参考**: https://x.com/asobodesign/status/2095785069550170313

当時のウェブの空気感を、1枚の HTML に驚くほど丁寧に落とし込んだ素晴らしいツール。
工事中バー、電光掲示板、アクセスカウンター、キリ番、相互リンクバナー、BGM 再生ボタンに至るまで、
「あの頃」の要素が外部ライブラリなしで再現されています。

[公式ライセンス情報](https://amix-design.com/asoboad/tools/d-dasaweb/license.html)では、生成された HTML の
ツール表記は削除してもよいと案内されていますが、素敵なツールへの敬意として記載を残しています。

生成された HTML 内のコメントおよび `<meta name="generator">` にも、ツール情報をそのまま残しています。

## 構成

```
.
├── public/
│   ├── index.html    # サイト本体（画像も base64 埋め込みの単一ファイル）
│   └── _headers      # セキュリティヘッダー定義
├── wrangler.jsonc    # Cloudflare Workers 設定
└── dasaweb-project.json  # ダサウェブ★メーカーのプロジェクトファイル（再編集用）
```

`dasaweb-project.json` は[ダサウェブ★メーカー](https://amix-design.com/asoboad/tools/d-dasaweb/)に読み込ませることで、
デザインや内容を再編集できます。

## 技術構成

Cloudflare Workers の静的アセット配信（Worker スクリプトなしの assets-only 構成）でホスティングしています。

- 外部リソースの読み込みは **ゼロ**（CDN・外部JS・外部CSS・Webフォントを一切使用せず、画像も base64 埋め込み）
- DNS レコードと TLS 証明書は Cloudflare が自動管理

## デプロイ

```bash
npx wrangler deploy
```

`public/index.html` を編集して上記を実行するだけで反映されます。

### セキュリティヘッダー

`public/_headers` で以下を付与しています。

| ヘッダー | 内容 |
| --- | --- |
| `Content-Security-Policy` | `default-src 'none'` を土台に、外部スクリプトの読み込みを全面禁止 |
| `X-Frame-Options` / `frame-ancestors` | クリックジャッキング対策 |
| `X-Content-Type-Options` | MIME スニッフィング防止 |
| `Referrer-Policy` | `strict-origin-when-cross-origin` |
| `Permissions-Policy` | 位置情報・カメラ・マイク・決済 API を無効化 |
| `Strict-Transport-Security` | HTTPS 強制（1年） |

> **注意**: CSP の土台が `default-src 'none'` のため、外部の JS や Web フォントを追加すると
> 読み込みがブロックされます。その場合は `public/_headers` の CSP も併せて更新してください。

## 権利・利用条件

このリポジトリ全体に、MIT License などのオープンソースライセンスは付与していません。

- HTML・CSS・JavaScriptの一部は、トミナガハルキさん制作の
  [ダサウェブ★メーカー](https://amix-design.com/asoboad/tools/d-dasaweb/)から生成されたものです。
  生成物や関連素材の取り扱いについては、同サービスの
  [公式ライセンス情報](https://amix-design.com/asoboad/tools/d-dasaweb/license.html)および
  [利用規約](https://amix-design.com/term/tools)をご確認ください。
- 当社が用意した文章・写真・リンクなどのコンテンツに関する権利は、株式会社hogehogeまたは
  それぞれの権利者に帰属します。
- サービス名、会社名、商標などに関する権利は、それぞれの権利者に帰属します。

このリポジトリの内容を転載・再配布・商用利用する場合は、各権利者の利用条件をご確認ください。
