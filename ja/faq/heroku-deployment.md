---
title: Heroku へデプロイ
description: Heroku へデプロイするには？
---

# Heroku へデプロイするには？

[Node.js 向けの Heroku のドキュメント ](https://devcenter.heroku.com/articles/nodejs-support)を読むことをお勧めします。

<div class="Promo__Video">
  <a href="https://vueschool.io/lessons/how-to-deploy-nuxtjs-to-heroku?friend=nuxt" target="_blank">
    <p class="Promo__Video__Icon">
      Vue School で <strong>Nuxt.js を Heroku にデプロイする方法</strong>についての無料レッスンをみる
    </p>
  </a>
</div>

まず `npm run build` を実行できるようにするために、Heroku にプロジェクトの `devDependencies` をインストールすることを伝える必要があります:

```bash
heroku config:set NPM_CONFIG_PRODUCTION=false
```

また､アプリケーションにホスト `0.0.0.0` を listen させプロダクションモードで起動します:

```bash
heroku config:set HOST=0.0.0.0
heroku config:set NODE_ENV=production
```

下記は Heroku ダッシュボードの Settings セクションに表示されています:

![nuxt config vars Heroku](https://i.imgur.com/EEKl6aS.png)

それから `package.json` 内の `heroku-postbuild` スクリプトを使って、Heroku に `npm run build` を実行するよう伝えます:

```js
"scripts": {
  "dev": "nuxt",
  "build": "nuxt build",
  "start": "nuxt start",
  "heroku-postbuild": "npm run build"
}
```

Heroku はアプリの dyno によって実行されるコマンドを指定する [Procfile](https://devcenter.heroku.com/articles/procfile) (ファイル拡張子を付けずにファイル名を `Procfile` という名前にします）を使用します。Procfile を起動するのはとてもシンプルで、以下の行を含める必要があります:

```
web: nuxt start
```

これは `nuxt start` コマンドを実行するように指示し、heroku に外部 HTTP トラフィックを向けるように伝えます。

最後にアプリケーションを Heroku に git push します:

```bash
git push heroku master
```

Heroku に master ではないブランチをデプロイするには次のようにします:

```bash
git push heroku develop:master
```

`develop` はあなたのブランチの名前です。

やりました！これで Nuxt.js アプリケーションは Heroku でホストされるようになりました！
