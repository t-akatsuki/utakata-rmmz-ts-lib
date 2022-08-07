# utakata-rmmz-ts-lib
RPGツクールMZにてTypeScriptを利用する際に競合してしまう標準型定義の調整を行うパッケージです。

TypeScriptはMicrosoft社が開発しメンテナンスしているオープンソースのプログラミング言語です。

https://github.com/microsoft/TypeScript

本型定義ではRPGツクールMZでTypeScriptを利用する際に障壁となる、グローバルオブジェクト定義の競合を対処するものです。  
TypeScriptに標準具備されている`lib-dom.d.ts`に対して競合部分を書き換えたものになります。  
TypeScript 4.5以降で導入された標準libのオーバーライドを利用する事で競合問題を解決します。

- TypeScriptはApache License, Version 2.0の下で提供されており、改変対象としている`lib-dom.d.ts`も同様です。

## 使い方
まだまだ調整箇所がある為、現在はパッケージとして提供していません。  
ローカルにダウンロードし、`npm install`にてローカルファイルからインストールしてください。

```shell
# ダウンロードしディレクトリを対象にnpm installする
$ npm install -D utakata-rmmz-ts-lib
```

- 【注意】このリポジトリにはRPGツクールMZの型定義は含まれません。

## 具体的な変更点
### Window定義の競合
`Windows`は`rmmz_core.js`内の定義と重複する。  
これはグローバルオブジェクトの`window`とは全くの別物である。

`lib.dom.d.ts`内におけるグローバルオブジェクトの`window`のinterface定義が`Window`となっている為に競合してしまう模様。

> `interface Window`を`interface GlobalWindow`と名称変更する事で対応。  
> RPGツクールMZの定義で上書きされてしまい宣言と矛盾する為、`declare var Window`宣言をコメントアウトする事で対応。

### StorageManager定義の競合
`StorageManager`は`rmmz_managers.js`内の定義と重複する。  
実験的な機能である為オミットする。

https://developer.mozilla.org/ja/docs/Web/API/StorageManager

> RPGツクールMZの定義で上書きされてしまい宣言と矛盾する為、`StorageManager`の定義部分/参照箇所をコメントアウトする事で対応。
