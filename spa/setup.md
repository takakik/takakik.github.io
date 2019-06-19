# react.js + babel + webpack + redux ( + jest.js)

## 目的
- jsx(React)を使うためにbabelを入れる
- JSファイルをまとめることができる

## 副産物
- 新しい言語仕様で記述したJSがいろんなブラウザ動く（互換性）
 - Write once, run anywhere
 - letなどが使えて便利
- babel + webpackでECMAScript Modulesをまとめたい

## 開発環境を構築
~/s4b_mobileでプロジェクトの初期化。
```
npm init -y
```
webpack, babelなどの開発ツールなどを、devDependenciesに追記したいため-D(--save-dev)オプションを付けてインストール。
```
npm install -D webpack webpack-cli babel-loader @babel/core  @babel/preset-env @babel/preset-react --no-bin-link
```
※vagrant上では、`--no-bin-link`を付けないとErrorになる。

実行用の「react」と「react-dom」を、dependenciesに追記したいため--saveオプションを付けてインストール
```
npm install --save react react-dom
```

webpack.config.jsを作成する。
ポイントは、各プロパティで以下を設定。
entry:束ね元
output:束ね先
module.rules.use.loader:babel-loaderを使う
module.rules.use.options.presets:@babel/preset-en @babel/react

webpack.config.js
```javascript
module.exports = {
  mode : "development",
  entry : "./src/main.js",
  output : {
    path : __dirname + "/public",
    filename : "bundle.js"
  },

  module : {
    rules : [
      {
        test : /\.js$/,
        use : [
          {
            loader: "babel-loader",
            options: {
              presets: [
                "@babel/preset-env",
                "@babel/react"
              ]
            }
          }
        ]
      }
    ]
  }
};
```

拡張子jsxを使いたい場合には以下を追記。
```javascript
{
  test : /\.jsx$/,
  use : [
    {
     loader: "babel-loader",
        options: {
          presets: [
            "@babel/preset-env",
            "@babel/react"
          ]
        }
    }
  ]
}
```

```
npm install webpack-dev-server --save-dev --no-bin-link
```
ビルドコマンドとして、package.jsonに以下を追記。
```javascript
"start": "./node_modules/webpack-dev-server/bin/webpack-dev-server.js --hot --inline --watch-content-base --conten
t-base public/ --open-page index.html"
````

`npm run start`を実行すると開発用サーバが立ち上がる。
 また、vagrant上の環境ではlocalhost:8081でホスト側からアクセスできないので以下をwebpack.config.jsに追記。
```javascript
devServer: {
  contentBase: __dirname + '/public',
  host: "0.0.0.0"
}
```
 portを指定したい場合には以下のようにする。
 ```javascript
   devServer: {
    contentBase: __dirname + '/public',
    host: "0.0.0.0",
    port:8040
  },
 ```
 
`npm run build`だけでbundleできるように、package.jsonを編集。

```javascript
"scripts": {
    "build": "./node_modules/webpack/bin/webpack.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```

reduxを使いたい（使いたくなった）ので以下を実行。
 ```
 npm install --save redux react-redux
 ```

## Bootstrap
```
npm i -D style-loader css-loader --no-bin-link
npm i -S bootstrap jquery popper.js
```

## React Intl
```
npm i react-localization
```

```javascript
{
   test: /\.css$/,
   use: [
    "style-loader",
    "css-loader"
  ]
}
```

## ハマりポイント
* 名前空間
```
src/
|--app
|  |--index.js
|  `--App.jsx
`--index.jsx
```

index.js
```javascript
export * from './App';
```
App.jsx
```javascript
import React from 'react';

class App extends React.Component {
}
```
となっていたとする。

`export * from './App.jsx'`ではなく、`export * from './App'`にしたい場合、
webpack.config.jsに
```
resolve: {
  extensions: ['.js', '.jsx']
}
```
を追記。

* ルーティング
react-routerでルーティングがうまくいかない場合には、webpack.config.jsに
```
devServer: {
    historyApiFallback: true,
}
```
設定されているかを疑う！！

## 参考
https://ics.media/entry/16028/  
https://qiita.com/akirakudo/items/77c3cd49e2bf39da79dd  
https://qiita.com/riversun/items/d27f6d3ab7aaa119deab  
https://qiita.com/msykd/items/7e72c4a942610e39b317  
https://qiita.com/ryusaka/items/d9afdec9baf34b9b6e41  
https://ics.media/entry/17749/

