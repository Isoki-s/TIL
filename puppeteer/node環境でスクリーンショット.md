# Gulp環境でpuppeteerでスクリーンショットを撮る

## 前提


puppeteerをインストール

```
$ npm i puppeteer
```

gulp.js

```js
// puppeteer
const puppeteer = require('puppeteer');

(async () => {
  // ここでserveのtask入れる
  const BASE_URL = 'http://localhost:8080/';
  const BASE_DIST = 'dest/';
  const Pages = [
    "index",
    "pagename",
    "list.html",
    "hoge",
  ]

  const browser = await puppeteer.launch();
  const page = await browser.newPage();

  for(let i in Pages) {
    await page.goto(BASE_URL + Pages[i]);
    await page.screenshot({path: `Pages[i]`.png , fullPage: true});
  }

  await browser.close();
})();

```

編集中...