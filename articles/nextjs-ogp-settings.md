---
title: "Next.jsのOGP画像設定を初心者向けに解説：opengraph-image.pngの仕組み"
emoji: "🖼️"
type: "tech"
topics: ["nextjs", "ogp", "seo", "webdev"]
published: false
slug: "nextjs-ogp-settings"
---

Next.jsのOGP画像設定、特にルート階層に`opengraph-image.png`を置く機能について、初心者の方にも分かりやすく解説しますね。

## OGPってそもそも何？🤔

まず、OGP (Open Graph Protocol) とは、ウェブページの内容をSNS（X(旧Twitter)やFacebookなど）でシェアされたときに、そのページの**タイトル**、**説明文**、**画像**などを正しく伝えるためのルール（お約束事）のことです。

この設定がされていると、リンクがシェアされた時にただのURLではなく、上の画像のようにリッチなカード形式で表示されます。これにより、ユーザーの目に留まりやすくなり、クリックしてもらえる可能性がぐっと上がります。このカードに表示される画像が**OGP画像**です。

## Next.jsの便利なOGP画像設定機能

通常、OGP画像はHTMLの`<meta>`タグでページのURLを指定する必要があり、少し手間がかかります。

```html
<meta property="og:image" content="https://example.com/some-image.png" />
```

しかし、Next.js (特にApp Router) には、この設定をとても簡単にしてくれる仕組みがあります。それが、特定の名前の画像ファイルを特定のフォルダに置くだけで、自動的にOGP画像として設定してくれる機能です。

## 「ルート階層の`opengraph-image.png`」がデフォルトになる仕組み

ここからが本題です。Next.jsのプロジェクトの`app`ディレクトリ直下に`opengraph-image.png`（または`.jpg`など）という名前の画像ファイルを置いてみましょう。

```
my-next-app/
└── app/
    ├── opengraph-image.png  <-- コレです！
    ├── layout.tsx
    └── page.tsx
```

この場所に置かれた`opengraph-image.png`は、**サイト全体の「デフォルトOGP画像」**として機能します。

### どういうこと？

これを「**会社の代表電話番号**」に例えると分かりやすいかもしれません。

- **ルートの`opengraph-image.png`** = **会社の代表番号** 🏢
    
    - どの部署に電話すればいいか分からない時、とりあえず代表番号にかければ繋がりますよね。それと同じで、どのページのOGP画像を表示すればいいか指定がない場合、Next.jsは自動的にこの「代表」の画像を使ってくれます。
        
    - これにより、どのページがSNSでシェアされても、最低限この画像が表示されるため、「画像なし」という寂しい状態や、意図しない画像が表示されるのを防ぐことができます。いわば**セーフティーネット（安全網）**のような役割です。

### 各ページで個別の画像を設定する場合

もちろん、ページごとに違う画像を設定したい場合も簡単です。例えば、「会社概要」ページには会社のロゴを、「製品紹介」ページにはその製品の画像を表示したいですよね。

これは、各ページのフォルダに同じように`opengraph-image.png`を置くだけで実現できます。

```
my-next-app/
└── app/
    ├── opengraph-image.png      <-- サイト全体のデフォルト画像（代表番号）
    ├── layout.tsx
    └── page.tsx
    │
    └── about/                   <-- aboutページ用のフォルダ
        ├── opengraph-image.png  <-- aboutページ専用の画像（部署の直通番号）
        └── page.tsx
```

- **各ページの`opengraph-image.png`** = **部署の直通番号** 📞
    
    - `app/about/`に置かれた画像は、「会社概要」ページがシェアされた時だけ使われます。こちらが優先されるので、デフォルトの画像は使われません。
        
    - このように、Next.jsはより具体的な階層にある設定を優先してくれます。もし`app/about/`に画像がなければ、親である`app/`のデフォルト画像を探しに行く、という賢い動きをします。

## さらに高度な使い方：動的に画像を生成する

静的な画像ファイルだけでなく、`opengraph-image.tsx`というファイルを使うと、**動的にOGP画像を生成する**こともできます。例えば、ブログ記事のタイトルを画像の中に入れたり、ユーザーのプロフィール画像をOGP画像にしたり、といったことが可能になります。これは非常に強力な機能です。

## まとめ

- **`app/opengraph-image.png`** は、サイト全体の**デフォルト（予備）のOGP画像**として機能する。
    
- 各ページで個別のOGP画像を設定したい場合は、そのページのフォルダ（例：`app/about/`）に`opengraph-image.png`を置けばOK。そちらが優先される。
    
- この仕組みのおかげで、OGP画像の設定漏れを防ぎつつ、ページごとに最適な画像を簡単に設定できる。

Next.jsのこの機能は、開発者がSEOやSNSでの見え方を手軽に改善できるように作られた、とても親切な仕組みと言えるでしょう。ぜひ活用してみてください！✨

## 参考資料

### 1. Next.js 公式ドキュメント (最重要)

まずは公式の情報を確認するのが一番確実です。どのようなファイル名が使えるのか、画像の推奨サイズなど、基本的なルールがすべて記載されています。

- **opengraph-image (日本語ドキュメント)**
    
    - [https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image)
        
    - **内容**: `opengraph-image.jpg`, `opengraph-image.png` といった静的な画像ファイルの設定方法から、`opengraph-image.tsx` を使って動的にOGP画像を生成する方法まで、網羅的に解説されています。 Next.jsを学ぶ上でブックマーク必須のページです。

### 2. 日本語の分かりやすい解説記事

静的なOGP画像の設定から、動的な画像生成まで幅広くカバーしている、現在もアクセス可能な記事を選び直しました。

- **Zenn - OGPをNext.js App Roouterで実装してlocalhost上で確認する**
    
    - [https://zenn.dev/tomo_redx/articles/b2d1c13d3ff361](https://zenn.dev/tomo_redx/articles/b2d1c13d3ff361)
        
    - **内容**: App Routerでの基本的なOGP画像の実装方法に加え、ローカル環境でOGPの表示をどうやって確認するかまで解説してくれています。初心者の方がつまずきやすい「作ったはいいけど、どうやって確認するの？」という部分を解決してくれる良記事です。
        
- **Qiita - 【Next.js13 + Vercel】App RouterでOGPとアナリティクスの設定をしたい**
    
    - [https://qiita.com/k-sukesakuma/items/ec8ec37c89749ff6e296](https://qiita.com/k-sukesakuma/items/ec8ec37c89749ff6e296)
        
    - **内容**: OGP画像の設定方法が、`layout.tsx`にメタデータを記述するコードと共に非常にシンプルに解説されています。Vercelにデプロイする際の`metadataBase`の設定にも触れられており、公開を視野に入れている方にとって実践的な内容です。
        
- **Zenn - Next.js AppRouterで動的OGP画像を作成する**
    
    - [https://zenn.dev/sui_water/articles/82f15c7ed9d8ea](https://zenn.dev/sui_water/articles/82f15c7ed9d8ea)
        
    - **内容**: こちらは`opengraph-image.tsx`を使って、ブログ記事のタイトルなどを埋め込む「動的なOGP画像」の作り方に特化した記事です。静的な設定の次のステップとして挑戦する際に、とても参考になります。

### 3. Vercelの公式サンプル (上級者向け)

Next.jsを開発しているVercelが提供している、OGP画像生成の様々なパターンを試せる公式のサンプルです。

- **Vercel - OG Image Generation**
    
    - [https://og-playground.vercel.app/](https://og-playground.vercel.app/)
        
    - **内容**: 左側のエディタでJSX（HTMLライクな記法）を書くと、リアルタイムで右側にOGP画像がプレビュー表示されます。どんなデザインが可能なのか、インスピレーションを得るのに最適です。コードも公開されているので、実装の参考にもなります。

これらのサイトを参考にしながら、ぜひご自身のNext.jsプロジェクトでOGP設定を試してみてください。
