---
title: "さめがめを作ろう"
---

## つくるもの

- ブラウザで動くビンゴマシーンを作ります
- 超初心者向けで「とにかく動く」を目指します
- HTMLファイルひとつで完結するので気軽に始められます

## コードサンプルの見方

以降のコードサンプルは **追加した行** と **削除した行** が分かるように書いてあります。

先頭に ``+`` が表示されている行は新しく追加した行です。先頭の ``+`` は入力せず、その後ろを行末まで追加してください。

先頭に ``-`` が表示されている行は削除した行です。既に入力されている行を丸ごと削除してください。

次の例のように ``-`` の行（の塊）と ``+`` の行（の塊）が続けて書いてある場合は、その行を書き換えてください。

```diff html
 <!-- 「template」を「ビンゴマシーン」に書き換える -->
-  <title>template</title>
+  <title>ビンゴマシーン</title>
```

それでは作っていきましょう。

## テンプレートをダウンロードする

下のリンクを開くとDownload ZIPというボタンがあります。これをダウンロードして、中のHTMLのテンプレート（template.html）を自分で分かるところに保存してください。

[Vue.js single-file-HTML template](https://gist.github.com/idomshi/883cc00c9f3f8a0083e51e0cb96ae2d0)

迷ったらデスクトップに「ビンゴマシーン」というフォルダを作ってその中に入れればOKです。

### 動作確認をする

いまダウンロードしたHTMLファイルをブラウザのウィンドウにドラッグアンドドロップすると白いページが表示されると思います。
まだ何も表示するものを書いていないので白くてOKです。
これから1ステップ作業するごとにこのページをリロードして動作を確認していきましょう。

## 1.

```diff html
 <html lang="ja">
 <head>
   <meta charset="UTF-8">
-  <title>template</title>
+  <title>ビンゴ</title>
   <script src="https://unpkg.com/vue@3.2.37/dist/vue.global.js"></script>
   <style>
```
```diff html
 </head>
 <body>
   <div id="app">
+    <div class="table">
+      <div class="column">
+        <p
+          class="cell"
+          v-for="(v, i) of opened.slice(0, 15)"
+          :key="i"
+          :class="{ open: v }"
+        >
+          {{ i + 1 }}
+        </p>
+      </div>
+    </div>
 
     <!-- ↑ここに表示するものを書く。 -->
   </div>
```
```diff html
   <script>
     const App = {
       setup() {
+        const opened = Vue.ref([...Array(75)].map(() => false))
+
+        return {
+          opened,
+        }
 
         // ↑ここにJavaScriptを書く。
       },
```

## 2.

1. で作った ``<div><p>～</p></div>`` をあと4つコピーして数字を書き換えます。

```diff html
           {{ i + 1 }}
         </p>
       </div>
+      <div class="column">
+        <p
+          class="cell"
+          v-for="(v, i) of opened.slice(15, 30)"
+          :key="i"
+          :class="{ open: v }"
+        >
+          {{ i + 16 }}
+        </p>
+      </div>
+      <div class="column">
+        <p
+          class="cell"
+          v-for="(v, i) of opened.slice(30, 45)"
+          :key="i"
+          :class="{ open: v }"
+        >
+          {{ i + 31 }}
+        </p>
+      </div>
+      <div class="column">
+        <p
+          class="cell"
+          v-for="(v, i) of opened.slice(45, 60)"
+          :key="i"
+          :class="{ open: v }"
+        >
+          {{ i + 46 }}
+        </p>
+      </div>
+      <div class="column">
+        <p
+          class="cell"
+          v-for="(v, i) of opened.slice(60, 75)"
+          :key="i"
+          :class="{ open: v }"
+        >
+          {{ i + 61 }}
+        </p>
+      </div>
     </div>
 
     <!-- ↑ここに表示するものを書く。 -->
```

## 3.

```diff html
 </head>
 <body>
   <div id="app">
+    <div class="number">
+      <p class="the-number">{{ theNumber }}</p>
+      <p class="button" @click="nextNumber">NEXT</p>
+    </div>
     <div class="table">
       <div class="column">
         <p
```

```diff html
     const App = {
       setup() {
         const opened = Vue.ref([...Array(75)].map(() => false))
+        const theNumber = Vue.ref("")
+
+        const nextNumber = () => {}
 
         return {
           opened,
+          theNumber,
+          nextNumber,
         }
 
         // ↑ここにJavaScriptを書く。
```

## 4.

スタイルシートを書いて見た目を整えていきます。

```diff html
   <title>ビンゴ</title>
   <script src="https://unpkg.com/vue@3.2.37/dist/vue.global.js"></script>
   <style>
+    body, div, p {
+      margin: 0;
+      display: flex;
+      flex-wrap: nowrap;
+      box-sizing: border-box;
+      justify-content: space-around;
+      align-items: center;
+    }
+
+    #app {
+      width: 100%;
+      height: 100vh;
+      padding: 0.5rem;
+      gap: 0.5rem;
+    }
+
+    .button {
+      width: 100%;
+      height: 3rem;
+      flex-shrink: 0;
+      background-color: rgb(96, 165, 250);
+      color: white;
+      border-radius: 0.25rem;
+      cursor: pointer;
+    }
+
+    .column {
+      height: 100%;
+      flex-direction: column;
+    }
 
     /* ↑ここにCSSを書く。 */
   </style>
```

## 5.
```diff html
--- D:/repository/20220930_bingo/004.html	Sat Oct 29 16:32:48 2022
+++ D:/repository/20220930_bingo/005.html	Sat Oct 29 16:34:12 2022
@@ -36,6 +36,39 @@
       flex-direction: column;
     }
 
+    .number {
+      width: 62%;
+      flex-grow: 6;
+      height: 100%;
+      flex-direction: column;
+    }
+
+    .table {
+      flex-grow: 1;
+      height: 100%;
+      background-color: rgb(144, 181, 194);
+      flex-direction: row;
+    }
+
+    .the-number {
+      height: 100%;
+      font-size: 33vh;
+    }
+
+    .cell {
+      width: 3rem;
+      height: 3rem;
+      border-radius: 50%;
+      background-color: rgb(203, 213, 225);
+      color: rgb(100, 116, 139);
+      font-size: 1.25rem;
+    }
+
+    .open {
+      background-color: rgb(253, 224, 71);
+      color: rgb(161, 98, 7);
+    }
+
     /* ↑ここにCSSを書く。 */
   </style>
 </head>
```

## 6.

番号を抽出する処理を書いたら完成です。

```diff html
         const opened = Vue.ref([...Array(75)].map(() => false))
         const theNumber = Vue.ref("")
 
-        const nextNumber = () => {}
+        const nextNumber = () => {
+          if (opened.value.every((v) => v)) return
+
+          let val
+          do {
+            val = Math.floor(Math.random() * 75)
+          } while (opened.value[val])
+
+          opened.value[val] = true
+          theNumber.value = val + 1
+        }
 
         return {
           opened,
```
