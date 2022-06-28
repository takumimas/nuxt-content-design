[nuxt/content](https://content.nuxtjs.org/)を使用したブログのテンプレートです。

[デモ](https://masublog.net/)

デザインにBulma、検索にfuse.jsを使用しています。

# contentファイルの形式

設置ディレクトリ：content/post
ファイル名：{id}.json

形式

```
{
    "id": "投稿ID",
    "date": "投稿日（表示用）：2022/03/04",
    "publishedAt": "投稿日時（sort用）2022-06-12T12:39:08.130Z",
    "title": "記事タイトル",
    "body": "記事本文",
    "category": {
        "id": "カテゴリーID",
        "createdAt": "カテゴリー作成日（任意）",
        "updatedAt": "カテゴリー更新日（任意）",
        "publishedAt": "カテゴリー公開日（任意）",
        "title": "カテゴリータイトル",
        "link": "カテゴリーリンク"
    }
}
```

# その他

カテゴリーページは個別でコードを用意しています。

ページングの実装はしていません。

100件以上コンテンツがある場合は表示されません。

ライセンス：MITライセンス