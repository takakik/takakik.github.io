# react.js + babel + webpack ( + jest.js)

##  目的
- jsx(React)を使うためにbabelを入れる
- babel + webpackでECMAScript Modulesをまとめたい

##  副産物
- ES2019の仕様で記述したJSがIEに対応できる
 - 新しい言語仕様が使える
 - Write once, run anywhere

## 開発環境を構築
~/s4b_mobileでプロジェクトの初期化。
```
npm init -y
```
webpack, babelなどの開発ツールなどを、devDependenciesに追記したいため-D(--save-dev)オプションを付けてインストール。
```
npm install -D webpack webpack-cli babel-loader @babel/core @babel/preset-env @babel/preset-reac --no-bin-link
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
```
module.exports = {
  mode : "development",
  entry : "./src/main.js",
  output : {
    path : __dirname + "/public/dist",
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

`npm run build`だけでbundleできるように、package.jsonを編集。

```
"scripts": {
    "build": "./node_modules/webpack/bin/webpack.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```

## 参考
https://ics.media/entry/16028/  
https://qiita.com/akirakudo/items/77c3cd49e2bf39da79dd  

