# liff-airtable

## LINE 設定

### プロバイダ作成

- LINE Developers(https://developers.line.biz/console/)にログイン
- プロバイダを作成する

### LINE ログインチャンネル作成

- 作成したプロバイダ配下で LINE ログインチャンネルを作成
- チャンネル ID はメモする(LIFF アプリで使用する)
- 権限で PROFILE,CHAT_MESSAGE を許可
- LIFF タブで LIFF アプリを追加する
  - LIFF アプリをデプロイしてから設定でも OK

### Messaging API チャンネル作成

- 作成したプロバイダ配下で LINE ログインチャンネルを作成
- 応答メッセージ無効
- LINE Official Account Manager でリッチメニュー作成
- リッチメニューから LIFF アプリをリンクする
  - https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/

## Airtable

### アカウント作成

https://airtable.com/

### Base、テーブル作成

#### テーブル情報

- user

  - ユーザ ID
  - ニックネーム
  - 性別
  - 注文履歴
  - 誕生年
  - 登録日
  - シャンプーに求めるもの

- order

  - 購入番号
  - 購入者
  - 購入商品
  - 購入量
  - ロット情報
  - 購入日

- product

  - 商品名
  - 在庫状況
  - 商品カテゴリ
  - 販売量
  - ロット情報
  - 成分情報
  - 成分情報
  - 商品画像

### 認証情報取得

後で LIFF に設定するのでメモしておく

- Base
  - Base 画面の右上 Help -> API Documentation から取得 app から始まるやつ
- APIKey
  - https://airtable.com/account -> api から取得

## liff アプリセットアップ

```
npm install
```

### 設定ファイル作成

.env ファイルを作成し、以下の情報を入力し保存

```
VUE_APP_LIFF_ID=xxxxx
VUE_APP_AIRTABLE_APIURL="https://api.airtable.com/v0/"
VUE_APP_AIRTABLE_APIKEY=xxxxx
VUE_APP_AIRTABLE_BASE=xxxx
```

### ローカルでの起動方法

```
npm run serve
```

### ビルド(dist 配下にできる)

```
npm run build
```
