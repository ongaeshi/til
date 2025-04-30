1. 以下のコードをクリップボードにコピーします：
```js
javascript:(function(){
  const selectedText = window.getSelection().toString();
  const pageTitle = document.title;
  const pageURL = location.href;
  const markdown = (selectedText !== '') ?
    `[${pageTitle}](${pageURL})\n\n> ${selectedText}` :
    `[${pageTitle}](${pageURL})`;
  navigator.clipboard.writeText(markdown).then(() => {
    alert('Markdown形式で引用しました。');
  }).catch(err => {
    alert('Markdown引用に失敗しました。');
  });
})();
```
2. ブラウザのブックマークに適当なページを登録します。
	- 注: Safari の場合は https で始まるページである必要があります。
3. 登録したブックマークを編集し、「URL」欄に上記のコードを貼り付けます。
4. ブックマーク名は「Markdown引用」などにするとわかりやすいです。
5. Webページ上でテキストを選択し、登録したブックマークレットを実行すると、クリップボードにMarkdown形式で引用します。
