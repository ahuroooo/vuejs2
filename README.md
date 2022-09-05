# Vue.js バージョン2系入門

## 基本解説
Vue.js とは
- 「ヴュー・ドット・ジェイエス」と読みます。
- JavaScript フレームワークの一つで、主に、MVC(ModelView Controller)モデルの View 層を扱います。
- MVC から派生した MVVM(Model View ViewModel) アーキテクチャを採用していると言われます。
- よく比較されるものに、Angular, React.js などがあります。
- Angular に比べ、シンプルで学習コストは低いといわれています。
- ECMAScript 5 をサポートするブラウザで動作します。IE は IE9 以降が対象となります。
- 開発者用に、Vue Devtools という Chrome のDeveloper Tools の拡張機能が公開されています。 

## 基本構文の習得

以下はおすすめの参考ページです。

[とほほのVue.js入門](https://www.tohoho-web.com/ex/vuejs.html)

サンプルがコンパクトにまとめられています。まずはこちらを参考にしてください。

[公式ドキュメント](https://jp.vuejs.org/v2/guide/)

学習の中でVueについてわからないことがあればこちらで調べてください。

コードを動かすのはローカルでもいいですが、codepenを使うとコーディングと動作確認をブラウザだけで行えるのでぜひ利用ください
https://codepen.io/

**注意：最新版指定するとvueの3系が読み込まれてしまうので、2系を使う場合は以下のように書いてください**

```
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
↓
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>
```


基本を身につけるために以下のソースを書いて、動かしてみましょう

### Hello world!
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue TEST</title>
<!-- Vue.js を読み込む -->
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>
</head>
<body>

<div id="app-1">{{ message }}</div>  <!-- {{ message }} が Vueデータに置換される -->

<script>
var app1 = new Vue({
  el: '#app-1',                        /* #app-1 要素に対して Vue を適用する */
  data: { message: 'Hello world!' }    /* message という名前のデータを定義する */
})
</script>

</body>
</html>
```

**ミニ課題**

Hello Vue！ 
という文字を、Vueデータを使ってHello world!の下に表示させましょう。


### バリデーションフォーム
フォームに名前や電話番号などを入力している最中に、バリデーションチェックのメッセージが動的に表示される画面を見たことがないでしょうか。
Vueを使うとこういったバリデーションも手軽に実装できます。

``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue TEST</title>
<!-- Vue.js を読み込む -->
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>
</head>

<style>
#app-2 .error {
  color: red;
}
</style>
<body>
<div id="app-2">
  <input type="text" v-model="message">
  <div class="error" v-if="error.require">必須項目です。</div>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  watch: {
    message: function(newVal, oldVal) {
      this.error.require = (newVal.length < 1) ? true : false;
    }
  },
  data: {
    message: 'Hello',
    error: {
      require: false
    }
  }
})
</script>
</body>
</html>
```

**ミニ課題**

上記画面で、入力が10文字を超えた場合はエラーメッセージを表示するようにしてください。

### ループ表示
Vue.js にはかなりの数のディレクティブがあり、それぞれ独自に特別な機能を持っています。例えば、`v-for` ディレクティブを使えばアイテムのリストを配列内のデータを使って表示することができます


``` html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>
<div id="app-107">
  <ul>
  <li v-for="color in colorList">{{ color }}</li>
  </ul>
</div>
<script>
var app107 = new Vue({
  el: '#app-107',
  data: { colorList: [ 'Red', 'Green', 'Blue' ] }
})
</script>
```

**ミニ課題**

colorListの下にtodoListを表示させてください。

todoListの要素数は3つ以上で、内容は自由とします。

------------------

## 課題

### １．演算結果をリアルタイムで表示する
vue.jsを使用して以下の仕様で画面を作ってください。
三角形の面積をリアルタイムで計算する画面です。

- テキストボックスを2つ表示する（縦の長さと横の長さ）
- テキストボックスに入力された数字から、三角形の面積を計算し、以下の形式で画面内に表示する
「縦2cm × 横3cm の三角形の面積は 3平方cm」
- 縦または横の数字を変更すると面積に反映される
- 数字以外の文字が入力されて計算出来ない場合は、バリデーションエラーメッセージを表示する

### ２．APIを使った住所検索
　
郵便番号を入力してボタンを押すと、住所を表示する画面を作成してください。
以下が課題の仕様です。記載のない部分については自由に作って大丈夫です。

- 以下オブジェクトを画面に表示します
　- 郵便番号入力テキストボックス
　- 住所検索ボタン
　- 都道府県表示テキストボックス
　- 住所表示テキストボックス
- 住所検索には[こちらのAPI](https://zipaddress.net/)を使用します
- API実行には[axios](https://jp.vuejs.org/v2/cookbook/using-axios-to-consume-apis.html)を利用します
- 郵便番号を入力して住所検索ボタンを押すと、APIを実行する
- APIで取得した都道府県を都道府県表示テキストボックスに、住所を住所表示テキストボックスに表示します
- 郵便番号が7桁でない場合はバリデーションエラーメッセージを表示する

------------------


より詳しく学ぶには、以下の公式マニュアルも参照ください

https://jp.vuejs.org/v2/guide/
