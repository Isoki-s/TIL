# Nuxt + GitHub Pages + TravisCI

## Githubでアクセストークンを取得

[Githubトークン設定](https://github.com/settings/tokens)から取得  
Scopeは`public_repo: Access public repositories`のみ


![Githubトークン設定](https://github.com/Isoki-s/TIL/blob/master/img/png/nuxt-githubpage-travis.png)

## githubpageを有効化する

GitHubのリポジトリの設定画面へ。

```
https://github.com/<username>/<repository-name>/settings
```

![Githubトークン設定](https://github.com/Isoki-s/TIL/blob/master/img/png/nuxt-githubpage-travis2.png)

githubpage sourceをmasterにしてsave

## TravisCI

[登録](https://travis-ci.org/)

Github連携を行う。リポジトリ一覧がでてくるので、トグルをオンに。

![Githubトークン設定](https://github.com/Isoki-s/TIL/blob/master/img/png/nuxt-githubpage-travis3.png)

RepositoryのSettingsを開き、Environment Variablesで`GITHUB_ACCESS_TOKEN`に先ほど取得したアクセストークンを入れます。

![GITHUB_ACCESS_TOKEN](https://github.com/Isoki-s/TIL/blob/master/img/png/nuxt-githubpage-travis4.png)


## GitHub Pages用の設定をNuxtプロジェクトに追加
GitHub PagesのURLは基本以下になる。

```
https://<username>.github.io/<repository-name>
```

nuxtのroute設定は/になるので変更が必要。
DEPLOY_ENVがGH_PAGESのときのみ、routerのBASEがリポジトリ名となるようにします。

``` nuxt.config.js
// `DEPLOY_ENV` が `GH_PAGES` の場合のみ `router.base = '/<repository-name>/'` を追加する
const routerBase = process.env.DEPLOY_ENV === 'GH_PAGES' ? {
  router: {
    base: '/<repository-name>/'
  }
} : {}

module.exports = {
  ...routerBase
}
```

## Travisの設定ファイルを追加

次にtravisの設定ファイルを追加します。

``` travis.yml
language: node_js
node_js:
  - "8"

cache:
  directories:
    - "node_modules"

branches:
  only:
  - master

install:
  - yarn install
  - DEPLOY_ENV=GH_PAGES yarn run generate

script:
  - echo "Skipping tests"

deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GITHUB_ACCESS_TOKEN
  target-branch: gh-pages
  local-dir: dist
  on:
    branch: master
```

DEPLOY_ENV=GH_PAGESにすることでGitHub Pages用の設定が有効になり、アクセストークンは環境変数の$GITHUB_ACCESS_TOKENから取得してくれる。

以降コミットすると、TravisCIがCommitをトリガーに自動デプロイしてくれるようになる。

## Github Pagesのbranchを切り替える

Github Pagesはmasterブランチでbuildされているため、これをgh-pagesに変更。githubpage sourceをgh-pagesにしてsave。再ビルド