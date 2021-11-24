# what's svelte.js

Svelte.jsは2016年にRich Harrisによって開発されたJavascript FrameWorkです。

以下は、[公式ドキュメント](https://svelte.dev/)からSvelteのコンセプトについて、引用したものです。

> *Svelteは、ユーザーインターフェイスを構築するための急進的な新しいアプローチです。ReactやVueのような従来のフレームワークは、ほとんどの作業をブラウザで行いますが、Svelteは、その作業を皆さんがアプリを構築するときのコンパイルステップに移動します。*
> 

上記の通り、Svelte.jsはWebアプリケーションやUIを構築するためのライブラリですが、従来のフレームワークとは異なり、UIライブラリではなくコンパイラです。

（詳細については後述します。）

また、svelteファイルはVue.jsのように一つのファイルに、HTML,CSS,Javascriptを記述してUIコンポーネントを構築します。

次にsvelteがもつ、3つの特徴を紹介いたします。

# Features of Svelte.js

Svelteには従来のフレームワークとの大きな違いとして3点あげています。

公式ドキュメントから引用します。

## Write less code(より記述量を少なく)

Svelte.jsの特徴として「小さくて速い」と言われています。

Svelte.jsはUIの構築をするコードの記述量を少なくするために、双方向バインディングやstateの管理などがシンプルに実装できるなど、様々な仕組みが備わっていて、

また、実行時のファイルサイズもJavascriptフレームワークの中では最小と言われています。以下が、[RealWorld](https://www.freecodecamp.org/news/a-realworld-comparison-of-front-end-frameworks-with-benchmarks-2019-update-4be0d3c78075/)から引用したグラフになります。

![スクリーンショット 2021-11-12 18.23.44.png](what's%20svelte%20js%205b6b10b78ab74d0b9de7f5bf6c8a822a/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2021-11-12_18.23.44.png)

## **No virtual DOM(仮想DOMを使用しない)**

このセクションを理解するには、仮想DOMへの理解が必要です。

公式ドキュメントがわかりやすかったため引用します。

### 仮想DOMって何？([公式ドキュメント](https://svelte.jp/blog/virtual-dom-is-pure-overhead)から引用)

JSXを使用した以下のような、Reactコンポーネントがあります。

```jsx
function HelloMessage(props) {
  return (
    <div className="greeting">
      Hello {props.name}
    </div>
  );
}
```

JSXを使用しなかった場合は以下のようになります。

```jsx
function HelloMessage(props) {
  return React.createElement(
    'div',
    { className: 'greeting' },
    'Hello ',
    props.name
  );
}
```

上記のコードは、ページがどのように見えるかを表現するオブジェクトになります。

このオブジェクトが仮想DOMです。

仮想DOMは、stateの値が更新されるたびに(例えば `props.name`  が変わったとき)、新たに作成されます。

フレームワークの仕事は、新しい仮想DOMと古い仮想DOMを*調整*し、どのような変更が必要か把握して、実際のDOMに仮想DOMを適用することです。

### 仮想DOMとSvelte.js

前述では仮想DOMについて説明しました。

ですが、仮想DOMの操作は、実際のDOMに対する最終的な操作に加えて行われる為、必要に応じて生のDOMとDOM APIを使えば仮想DOMを使用したフレームワークにパフォーマンス的に勝つことができます。

本題は戻り、Svelte.jsは仮想DOMを使用しません。

従来のjavascriptフレームワークは、実行時にコードを解釈しますが、Svelteはビルド時に差分を検知し、その差分のコードをプレーンなJavaScript(HTML,CSS)にコンパイルをします。ランタイムもより、高速になります。

## **Truly reactive(Reactive)**

Svelteはビルド時に、DOMの更新を行う非常に効率的な命令的なコードに変換します。

これに関しては、実際にコードを見た方がわかりやすいかと思いますので、早速セットアップから始めていきましょう。

## Svelte.jsのセットアップ

** CDNはありません（2021/11/15現在）**

### 前提

Node.jsがインストールされている必要があります。

またプロジェクト作成には、npxコマンドを使用します。

### 環境

M1 Macを使用しています。

MacOS: 11.5.1(macOS Big Sur)

Node.js: 14.17.6

npm: 6.14.15

svelte: 3.0.0

### セットアップ手順

Svelte.jsのインストールは、以下のコマンド達をコマンドラインで実行してください。

(今回はcssをsassを使用して書くのでsassもインストールします。)

```jsx
npx degit sveltejs/template {training-svelte} ←ここは任意のプロジェクト名を入力してください。

npm i -D sass node-sass
```

> コマンド内で使用されている「npx」コマンドについては[こちら](https://zenn.dev/ryuu/articles/what-npxcommand)を参考にしてください。
> 

上記コマンドを実行した後の、プロジェクトは[このような構造](https://github.com/Apro-yuto/training-svelte/commit/0fa2f5ec2f8e1a7e1bddb5481109b862f1f3c9d0)になっています。

この状態でも、動作するためブラウザの表示確認をしてインストールを完了としたいと思います。

以下のコマンドを実行して、ブラウザでの表示確認をしていきます。

```jsx
npm run dev
```

[http://localhost:5000](http://localhost:5000/)にアクセスして、表示が確認できました。

![スクリーンショット 2021-11-21 1.27.46.png](what's%20svelte%20js%205b6b10b78ab74d0b9de7f5bf6c8a822a/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2021-11-21_1.27.46.png)

## TODOアプリ作成

インストールとセットアップが完了したため、Svelteの使い方を把握するために簡単なTODOアプリを作成していきます。

Svelteは単一ファイルコンポーネントで書けるため、コンポーネント毎に説明して行きます。（reset.css読み込み等の作業は済んでいる想定で進めます。詳しくは、[Github](https://github.com/Apro-yuto/training-svelte)を参照ください）

※ベースのコンポーネントは以下のようになります。

このコンポーネントにコンポーネントをインポートしてアプリケーションを構築していきます。

```jsx
<script>
</script>

<main>
</main>

<style>
</style>
```

### ヘッダー・共通コンポーネント作成********************************注

まず共通コンポーネントである、ヘッダーコンポーネントを作成します。

```jsx
<header class="header">
  <a href="/" class="header_logo">
    <img src="img/logo.png" alt="LOGO">
  </a>
</header>

<style>
.header {
  width: 100%;
  background-color: #fff;
  padding: 20px 0;
}
.header_logo {
  width: 50px;
  display: block;
  margin: 0 auto;
}
</style>
```

・・・普通のコーディングです。

![スクリーンショット 2021-11-24 1.54.01.png](what's%20svelte%20js%205b6b10b78ab74d0b9de7f5bf6c8a822a/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2021-11-24_1.54.01.png)

↑ちなみに表示は、上のようになってます。（ロゴは自作しました。...といっても[こちらのサイト](https://hatchful.shopify.com/ja/)から自分で生成しました。）

### コンテンツ部分の作成 - フォームコンポーネント -

次にコンテンツ部分を作成します。まずはTODOを追加するフォームコンポーネントを作成します。

TODOを追加する機能を実装するためTODO全体をグローバルで使用できるよう、状態管理を使用します。

vueで言うと、Vuex。reactで言うと、reduxに当たります。

Svelteでは、標準搭載のsvelte/storeを使用することで、Storeパターンでの状態管理を開始できます。

今回はTODO全体を管理するだけなので、以下のように書きました。

```jsx
import { writable } from 'svelte/store'

export const todo = writable([])
```

writableメソッドを使用することで、storeを使用できます。
