# react.js + babel + webpack ( + jest.js)

##  目的
- jsx(React)を使うためにbabelを入れる
- babel + webpackでECMAScript Modulesをまとめたい

##  副産物
- ES2019の仕様で記述したJSがIEに対応できる
 - 新しい言語仕様が使える
 - Write once, run anywhere

## 開発環境を構築
~/s4b_mobileで以下を実行。
`npm init -y`

vagrant上では、`set-env --no-bin-link`を付けないとErrorになる。
`npm install -D webpack webpack-cli babel-loader @babel/core @babel/pre
set-env --no-bin-link`

webpack.config.jsを作成する。
outputプロパティで束ね先を設定。

```
module.exports = {
  mode : "development",
  entry : "./src/index.js",
  output : {
    path : __dirname + "/public/dist",
    filename : ".js"
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
                "@babel/preset-env"
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
