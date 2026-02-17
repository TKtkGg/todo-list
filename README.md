# TODO リスト アプリケーション

JavaScript学習用のシンプルなTODOリストアプリケーションです。VanillaJavaScript（フレームワークを使わないJavaScript）を使用して、DOM操作の基本を学ぶことができます。

## 機能

- TODOの追加
- TODOを未完了リストから完了リストへ移動
- 完了したTODOを未完了リストに戻す
- TODOの削除

## JavaScriptで実装している内容

### 1. DOM操作の基本

#### 要素の取得
```javascript
document.getElementById("add-text")
```
`getElementById`を使って、HTML要素をIDで取得しています。

#### 要素の動的生成
```javascript
const li = document.createElement("li");
const div = document.createElement("div");
const p = document.createElement("p");
const button = document.createElement("button");
```
`createElement`メソッドで、JavaScriptから新しいHTML要素を作成しています。

#### 要素の属性設定
```javascript
div.className = "list-row";
p.innerText = todo;
```
生成した要素に対して、CSSクラスやテキストコンテンツを設定しています。

### 2. イベントリスナー

#### クリックイベントの登録
```javascript
document.getElementById("add-button").addEventListener("click", onClickAdd);
```
ボタンがクリックされたときに実行される関数を登録しています。

#### 動的に生成された要素へのイベント登録
```javascript
completeButton.addEventListener("click", () => {
    // 完了処理
});
```
動的に作成したボタンにもイベントリスナーを追加し、各TODO項目ごとに独立した動作を実現しています。

### 3. DOM要素の追加・削除

#### 要素の追加
```javascript
div.appendChild(p);
document.getElementById("incomplete-list").appendChild(li);
```
`appendChild`メソッドで、親要素に子要素を追加しています。

#### 要素の削除
```javascript
completeButton.nextElementSibling.remove();
document.getElementById("incomplete-list").removeChild(deleteTarget);
```
`remove()`メソッドや`removeChild()`メソッドで、DOM要素を削除しています。

### 4. DOM要素の検索

#### 親要素の検索
```javascript
const moveTarget = completeButton.closest("li");
```
`closest`メソッドを使って、クリックされたボタンから一番近い親の`<li>`要素を取得しています。

#### 兄弟要素・子要素の取得
```javascript
completeButton.nextElementSibling.remove();
moveTarget.firstElementChild.appendChild(backButton);
```
- `nextElementSibling`: 次の兄弟要素を取得
- `firstElementChild`: 最初の子要素を取得

### 5. クロージャ（重要な概念）

```javascript
const createIncompleteTodo = (todo) => {
    const completeButton = document.createElement("button");
    completeButton.addEventListener("click", () => {
        // ここで外側の関数の変数todoにアクセスできる
        createIncompleteTodo(todo);
    });
};
```
イベントリスナー内で、外側の関数スコープの変数（`todo`）にアクセスできています。これはJavaScriptのクロージャという機能によるもので、関数が作成された時の環境を保持しています。

### 6. アロー関数の使用

```javascript
const onClickAdd = () => {
    // 処理
};
```
ES6のアロー関数記法を使用しています。従来の`function`キーワードよりも簡潔に関数を定義できます。

### 7. 条件分岐

```javascript
if(inputText){
    createIncompleteTodo(inputText);
}
```
空のTODOが追加されないように、入力値がある場合のみ処理を実行しています。

## 技術スタック

- HTML5
- CSS3
- JavaScript（ES6+）
- Vite（開発サーバー・ビルドツール）

## 学習ポイント

このアプリケーションを通して、以下のJavaScriptの基本を学べます：

1. **DOM操作**: Webページを動的に変更する方法
2. **イベント処理**: ユーザーの操作に応答する方法
3. **要素の動的生成**: JavaScriptでHTMLを作成する方法
4. **クロージャ**: 関数スコープとデータの保持
5. **関数型プログラミング**: アロー関数の使用
6. **Webアプリケーションの基本構造**: HTML/CSS/JavaScriptの連携

## 開発

このプロジェクトはViteを使用しています。開発サーバーは自動的に起動します。

ビルドコマンド:
```bash
npm run build
```