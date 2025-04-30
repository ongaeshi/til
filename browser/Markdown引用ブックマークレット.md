Webページの内容をMarkdown形式で引用するブックマークレットの設定方法。

1. 以下のコードをクリップボードにコピー：

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

2. ブラウザのブックマークに任意のページ（このページなど）を登録
   - Safari の場合は https で始まるページが必要

3. 登録したブックマークを編集し、「URL」欄に上記のコードを貼り付け

4. ブックマーク名を「Markdown引用」などに変更

5. Webページ上でテキストを選択し、登録したブックマークレットを実行すると、クリップボードにMarkdown形式で引用される

# 関連記事
- [Markdownコピーブックマークレット](./Markdownコピーブックマークレット.md)
