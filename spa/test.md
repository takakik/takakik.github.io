## setup

```
npm i -D jest --no-bin-links
```

```
npm i -D puppeteer --no-bin-links
```

下も環境によっては実行する必要があるかも
```
sudo apt-get install libnss3
```
```
sudo apt-get install libxss1
```

puppeteerの起動、終了をするための下記ファイルを作成[*](https://jestjs.io/docs/ja/puppeteer){:target="_blank"}

```
jest.config.js setup.js teardown.js
```
