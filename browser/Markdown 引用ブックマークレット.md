1. 以下のコードをクリップボードにコピーします：
```js
javascript:(function(){
  const selectedText = window.getSelection().toString();
  const pageTitle = document.title;
  const pageURL = location.href;
  const markdown = `[${pageTitle}](${pageURL})\n\n> ${selectedText}`;
  navigator.clipboard.writeText(markdown).then(() => {
    alert('Markdown形式で引用');
  }).catch(err => {
    alert('コピーに失敗しました');
  });
})();
```
2. ブラウザのブックマークに適当なページを登録します。
	- 注: Safari の場合は https で始まるページである必要があります。
3. 登録したブックマークを編集し、「URL」欄に上記のコードを貼り付けます。
4. 名前は「Markdown引用」などにするとわかりやすいです。
5. Webページ上でテキストを選択し、登録したブックマークレットを実行すると、クリップボードにMarkdown形式でコピーできます。
