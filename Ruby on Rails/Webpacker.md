# webpack
- Webアプリケーションを作成するのに必要なJavaScriptをまとめて管理するためのツール。
- webpackによって、JavaScriptのライブラリとその他の言語を変換・圧縮した上で好きな位置に配置できる。
- WebpackerはwebpackをRuby on Rails仕様にしたGemのこと。

# WebpackerでjQueryを管理する
## jQueryのインストール方法
- yarn addによりpackage.jsonに自動でバージョンが書き込まれる。
- Gemfileにgem 'jquery-rails'、bundle installでも導入可。
```
$ % yarn add jquery
```

- config/webpack/environment.js
```
const { environment } = require('@rails/webpacker')
const webpack = require('webpack')

environment.plugins.prepend('Provide',
  new webpack.ProvidePlugin({
    $: 'jquery',
    jQuery: 'jquery',
    jquery: 'jquery',
  })
)

module.exports = environment
```

- app/javascript/packs/application.js （jQueryの呼び出し）
```
require("@rails/ujs").start()
require("turbolinks").start()
require("@rails/activestorage").start()
require("channels")
require('jquery')
```

- application.html.erbでデフォルトでJavaScriptの読み込みができている。
- JavaScriptディレクトリ直下にjsファイルを作成し、動作を記述後、app/javascript/packs/application.jsにそのjsファイルの読み込みをする。
