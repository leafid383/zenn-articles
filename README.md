# Fumi's Zenn Articles

このリポジトリはZennで公開する技術記事を管理しています。

## 構成

```
zenn-articles/
├── articles/          # Zenn記事
├── books/            # Zenn本
├── images/           # 記事用画像
├── scripts/          # 管理スクリプト
└── .github/workflows/ # CI/CD
```

## 使い方

### ローカルプレビュー
```bash
npm run preview
```

### 新しい記事作成
```bash
npm run new:article
```

### 記事一覧確認
```bash
npm run list
```

## 記事管理フロー

1. Obsidianで記事執筆
2. `06_Articles/ready/` に移動
3. 同期スクリプトで自動変換・公開

## 連携

- **Obsidianリポジトリ**: `/Users/fumi/Repos/notes`
- **同期方向**: Obsidian → Zenn（一方向）
- **GitHub連携**: 自動デプロイ設定済み

## 注意事項

- このリポジトリは公開用です
- 下書きも含めて全て公開されます
- プライベートな内容はObsidianリポジトリで管理してください
