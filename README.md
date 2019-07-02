# Nuxt-univ-Firebase-hostting 
NuxtアプリケーションをCircleCIでFirebaseに自動ディプロイする。
 xxxx

#GitHub 
## GitHubリポジトリをcloneしてローカルプロジェクト作る。 
1. 新規ローカルプロジェクトのディレクトリを作成する
2. リモートリポジトリをcloneする。 
```
    git clone https://github.com/hiramatsuYoshiaki/nuxt-univ-app2.git  
```
3. インストールする  
```
    npm install  
```
4. サーバーを立ち上げて確認    
```
   npm run dev
```
5. ローカルサーバーへアクセス 
```
   http://localhost:3000/で確認する。 
```
 
## GitHub 新規リモートリポジトリの作成 
1. GitHub ログイン後のトップページから、Repositories の New ボタンをクリックします。 
2. Create a new repository の画面に遷移するので、リポジトリ名、ライセンス等を入力。Initialize this repository with a READMEはチェックせず画面下のほうにある Create repository ボタンをクリックします。

## cloneしたリモートリポジトリから新規リモートリポジトリへURLを変更する
1. git remote -v
2. origin  https://github.com/hiramatsuYoshiaki/nuxt-univ-app2.git (fetch)  
3. origin  hhttps://github.com/hiramatsuYoshiaki/nuxt-univ-app2.git (push)  
4. git remote rm originで現在のリモートリポジトリを削除する  
5. git remote add originで新しいリモートリポジトリを追加する   
6. git remote add origin https://github.com/hiramatsuYoshiaki/プロジェクト名vue-cli3-unit-alprime.git
 
## ローカルプロジェクトを GitHub に Push する 
1. git add -A 
2. git commit -m "first commit" 
4. git push -u origin master 

## ローカルプロジェクトで現在のブランチから開発用の派生ブランチ(dev)を作成してGitHubへPushする。  
1. git branch new-branch(dev) 
2. git checkout new-branch(dev)
3. git branch 
   * dev 
     master 
4. git add -A 
5. git commit -m 'new branch dev commit' 
6. git push --set-upstream origin dev 
   (もしくは、　git push -u origin dev) 

## GitHubでDevブランチをmasterブランチにマージする
1. codeタグを選択し、branch:masterボタンを押し、開発用のブランチ（dev）を選択する。
2. New pull requestボタンを押す
3. Create pull requestボタンを押す
4. Confirm margeボタンを押す
5. Delete branchボタンを押す


# Firebaseで新規プロジェクトを作成しディプロイする。 
## 手動でディプロイする。
1. Firebaseで新規プロジェクトを作成する。 
 
2. Firebase CLI をインストール 
```
$ npm install -g firebase-tools 
```
 
3. Firebase プロジェクトにアクセスする 
```
$ firebase login
```
 
4. サイトを初期化する（firebasercとfirebase.jsonを作る） 
```
$ firebase init
```
  
選択肢に答える  
 
 ```
? Are you ready to proceed?
```
⇒　yを押して、enterを押す 

```
 
? Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to conf
irm your choices. Hosting: Configure and deploy Firebase Hosting sites
```
 
下矢印キーを押してリストを選択 
⇒　hostingを選択し、スペースキーを押して、enterを押す。(ホスティングのみ選択) 
```
? Select a default Firebase project for this directory:
``` 
 
下矢印キーを押してリストを選択（プロジェクト数が多い場合は下に隠れている） 
⇒　スペースキーを押してプロジェクトを選択して。enterを押す 
``` 

? What do you want to use as your public directory? 
```
⇒　distを入力し、enterを押す 
```
 
? Configure as a single-page app (rewrite all urls to /index.html)? 
```
⇒　nを入力し、enterを押す。（シングルページアプリケーションの場合はy） 
 
```
? File dist/index.html already exists. Overwrite? 
```
⇒　ｎを入力し、enterを押す 
 
5. アプリケーションのルートディレクトリにfirebasercとfirebase.jsonができていることを確認する。 
 
6. buildもしくは、generateする 
```
$ npm run build もしくは、npm run generate 
```
 
7. ローカルで実行してテストしてみる 
 
```
$ firebase serve 
```
localhost:5000/にアクセスして確認する 　
 
8. firebaseにディプロイする 
```
$ firebase deploy 
```
 
9. firebaseにホスティングされていることを確認する。 
https://nuxt-app-xxxx.firebaseapp.com/にアクセスするか、firebaseのダッシュボードからアクセスして確認する。 
  
 
## Circle CI で自動でディプロイ設定をする。 
https://qiita.com/nakata_kazuhiro/items/53c7f06900ae3156e07b 
https://note.mu/yoneapp/n/n7037373c0b76
  
1. プロジェクトで以下のコマンドを実行し、デプロイ用のFirebaseトークンを取得する。表示されたデプロイ用のFirebaseトークンはコピーしておく。 
```
 
$ firebase login:ci
```
2. CircleCIにログイン後、画面のサイドバーから「SETTINGS」を選択し、「projects」クリックしてGitHubリポジトリのリストを表示する。 
3. 該当するリポジトリの右端にある、歯車アイコンをクリックする。
 
4. BUILD SETTINGSの「Environment Variables」をクリックし、画面遷移する。 
  

5. 「Add Variable」ボタンを押し,順次以下の設定をポップアップ画面に入力する。 

firebaseトークンを設定する
```
nema:  FIREBASE_TOKEN 
value: xxxaoxnMhPCgF8SoK2ND6HDdh4G0-bKm-xxxxxxxxxxxx

```
 
firebaseプロジェクトIDを設定する
```
name:  FIREBASE_PROJECT_ID
value: nuxt-app-xxxxxxxx
```
 
firebaseConfigを設定する　
```
name:  FIREBASE_API_KEY
value: xxxxxxxxx_zE8_oNkN43OS-xhlIIAQv2uOjLTLI 
 
firebase ホスティングドメイン
name:  FIREBASE_AUTH_DOMAIN
value: nuxt-app-xxxx.firebaseapp.com
 
firebase データベースURL
name:  FIREBASE_DATABASEURL
value: https://nuxt-app-xxxx.firebaseio.com
 
 firebase プリジェクトID
name:  FIREBASE_PROJECTID
value: nuxt-app-xxxx
 
 firebase ストレージバケット
name:  FIREBASE_STORAGEBUCKET
value: nuxt-app-xxxx.appspot.com
```
 
# dotenv を使って環境変数を設定し、Firebaseのconfigで使う。
1. dotenvをインストール 
```
$ npm i @nuxtjs/dotenv
```
2. nuxt.config.jsを編集する 
`nuxt.config.js`
```
export default {
  modules: [
    '@nuxtjs/dotenv'
  ],
  env: {
    FIREBASE_API_KEY: process.env.FIREBASE_API_KEY,
    FIREBASE_AUTH_DOMAIN: process.env.FIREBASE_AUTH_DOMAIN,
    FIREBASE_DATABASEURL: process.env.FIREBASE_DATABASEURL,
    FIREBASE_PROJECTID: process.env.FIREBASE_PROJECTID,
    FIREBASE_STORAGEBUCKET: process.env.FIREBASE_STORAGEBUCKET,
  },
}
```
3. .envをルートディレクトリに作りキーを設定する。 
`.env`
```
FIREBASE_API_KEY='<key>'
FIREBASE_AUTH_DOMAIN='oauth3.firebaseapp.com'
FIREBASE_DATABASEURL='https://oauth3.firebaseio.com'
FIREBASE_PROJECTID='oauth3'
FIREBASE_STORAGEBUCKET='oauth3.appspot.com'
```
4. Firebase configにprocess.envを使って設定をする。
`plugins/firebase.js`
```
import firebase from 'firebase/app'
import 'firebase/database'
import 'firebase/firestore'
import 'firebase/auth'
import 'firebase/storage'
 
const config = {
  apiKey: process.env.FIREBASE_API_KEY,
  authDomain: process.env.FIREBASE_AUTH_DOMAIN,
  databaseURL: process.env.FIREBASE_DATABASEURL,
  projectId: process.env.FIREBASE_PROJECTID,
  storageBucket: process.env.FIREBASE_STORAGEBUCKET
}
 
if (firebase.apps.length === 0) {
  firebase.initializeApp(config)
}
 
export default firebase

```
 　

## config.ymlに自動でディプロイ設定をする。

1. CircleCIではnpm -gでのコマンド実行が出来ないため、グローバルインストールのみの場合は、pakage.jsonに追加するために、プロジェクトにインストールする。 　
 　
```
$ npm install --save-dev firebase-tools
$ npm install --save-dev @nuxtjs/dotenv
```
 

2. CircleCIの設定ファイルを作成
プロジェクト直下に`.circleci/config.yml`ファイルを作成します。(ファイル名の先頭に.を付ける点に注意) 　
 　
3. .circleci/config.ymlを編集する 
```
version: 2
jobs:
  deploy_dev: # ジョブ名
    docker:
      - image: circleci/node:10.15.3 # ジョブ実行環境のDockerイメージを記述
    steps:
      - checkout # ソースコードのチェックアウト
      - run:
          name: Add env # .envを作成　セキュリティためGitHubにはアップしないため
          command: |
            echo "FIREBASE_API_KEY=$FIREBASE_API_KEY" > .env
            echo "FIREBASE_AUTH_DOMAIN=$FIREBASE_AUTH_DOMAIN" >> .env
            echo "FIREBASE_DATABASE_URL=$FIREBASE_DATABASE_URL" >> .env
            echo "FIREBASE_PROJECT_ID=$FIREBASE_PROJECT_ID" >> .env
            echo "FIREBASE_STORAGE_BUCKET=$FIREBASE_STORAGE_BUCKET" >> .env
          # echo "FIREBASE_MESSAGING_SENDER_ID=$FIREBASE_MESSAGING_SENDER_ID" >> .env
      - run: # 順に実行したいコマンドとコマンドに名前をつけます
          name: npm install
          command: npm i
      - run:
          name: build
          command: npm run generate
      - run:
          name: deploy to Firebase Hosting
          command: ./node_modules/.bin/firebase deploy --project=$FIREBASE_PROJECT_ID --token=$FIREBASE_TOKEN # プロジェクト上のfirebase-toolsでデプロイします

workflows:
  version: 2
  deploy_dev: # ワークフローの名前
    jobs:
      - deploy_dev: # 上で定義したジョブを指定します
          filters:
            branches:
              only: dev # developブランチのみを実行対象とします。今回はdevブランチ
```
 
4. developブランチをビルド可能な状態でpushするとジョブが実行されます。
5. Circle CIのjobs画面で確認できます。 
6. https://nuxt-app-xxxx.firebaseapp.com/にアクセスしホスティングされていることを確認します。
 
  

 
# nuxt-univ-app1 
> My peachy Nuxt.js project
## reate-nuxt-app
```
$ npx create-nuxt-app nuxt-univ-app1
? Project name nuxt-univ-app1
? Project description My peachy Nuxt.js project
? Use a custom server framework express
? Choose features to install Axios
? Use a custom UI framework none
? Use a custom test framework none
? Choose rendering mode Universal
? Author name hiramatsu
? Choose a package manager npm
$ cd nuxt-univ-app1
$ npm run dev
```

## Build Setup

``` bash
# install dependencies
$ npm install 

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, checkout [Nuxt.js docs](https://nuxtjs.org).

*** 
# nuxt.config.js setting
> nuxt.config.jsでの導入時の設定
# eslint
フォーマットエラー対応
✖ 7 problems (7 errors, 0 warnings) 
  7 errors, 0 warnings potentially fixable with the `--fix` option. 
  
Solved adding fix option in nuxt.config.jsfile: 
```
extend(config, ctx) {
    if (ctx.dev && ctx.isClient) {
        config.module.rules.push({
            enforce : 'pre',
            test    : /\.(js|vue)$/,
            loader  : 'eslint-loader',
            exclude : /(node_modules)/,
            options : {
                fix : true
            }
        });
    }
}
```
ex.https://github.com/nuxt/nuxt.js/issues/1628 
```
options: {
fix: true
       }
```
 
 ***



# cssプロパティ 
sass を利用したい場合は node-sass および sass-loader パッケージをインストールしてください。 
1. install 
```
npm install --save-dev node-sass sass-loader
```
2. nuxt.config　setting 
```
export default {
  css: [
    // プロジェクト内の SCSS ファイル
    '@/assets/sass/styles.scss'
  ]
}
```
3. component style setting 
```
    <style scoped lang="scss">
    </style>
```
 
# SASS変数をvueファイルで使う 
importの記述なしで使う。
1. install 
```
npm install --save-dev @nuxtjs/style-resources
```
2. nuxt.config setting 
```
modules: [
    '@nuxtjs/style-resources',
  ],
  styleResources: {
    sass: [
      '~/assets/sass/variable.scss',
    ],
  },
```
3. usage 
```
<style scoped lang="scss">
//@import "../../../assets/scss/common/data/thema.scss";
.container {
    color: $text-color
}
</style>
```
# autoprefixer の設定をカスタマイズする
Nuxt.js で CSS(Sass) をコンパイルすると、 autoprefixer がベンダープレフィクスを自動で適用してくれます。 
1. nuxt.config setting 
```
build: {
  postcss: [
    require('autoprefixer')({
      browsers: ['IE 11', 'last 2 versions' ],
      grid: true
    })
  ]
}

```
2. autoprefixer デフォルト設定 
```
1%, last 2 versions, Firefox ESR
```
1%:1%以上のシェアがあるブラウザ 
last 2 versions:最後の2バージョンのブラウザ 
Firefox ESR:最新のFirefox ESR版  
3.対応ブラウザの確認
https://browserl.ist/?q=%3E+1%25%2C+last+2+versions%2C+Firefox+ESR 
  
参考ページ:https://parashuto.com/rriver/tools/using-custom-data-for-autoprefixer 

# Google Analytics
1. install 
```
npm install --save @nuxtjs/google-analytics
```
2.アナリティクスのトラッキング IDを設定する 
```
modules: [
  ['@nuxtjs/google-analytics', { id: 'UA-xxxxx-x' }],
],
```
# Google Serch Colsole
1. Google Serch Colsoleからメタタグを取得
2. nuxt.config setting
```
head: {
   
    meta: [
      { name: "google-site-verification",
        content: "TaWpD9i4R5GSPzJjnTc8--t-g8bbDKbfxQX-e1kgio0" },
    ],
  },
```

# Nuxt.jsで静的ファイル生成時にサイトマップも自動生成する方法
npm run generateで静的ウェブサイトを生成 
1. install 
```
npm install --save @nuxtjs/sitemap
```
2. nuxt.config.js setting 
```
modules: [
    '@nuxtjs/sitemap',
  ],
  sitemap: {
    // path: '/sitemaps.xml',//Default: sitemaps.xml
    hostname: 'https://romantic-kare-6d357c.netlify.com/',
    generate: true,
    // exclude: [
    //   '/admin'
    // ],
    routes:[
      "/",
      {
        url: '/works',
        changefreq: 'daily',
        priority: 1,
        lastmodISO: '2017-06-30T13:30:00.000Z'
      },
      "/about",
      "/contact"
    ]
  },
```
各パラメーターについて
path
生成されるサイトマップファイルの名前。
generateオプションでdirを変更していなければ、distフォルダの中に生成される。

hostname
サイト名。

generate
nuxt generate時に静的なサイトマップファイルを生成するかの設定。
ここをtrueにしておかないとサイトマップファイルが生成されないので注意。

exclude
サイトマップに含めたくないRULを指定できる。
管理者ページなどがある場合に使用する。

routes
サイトマップに含めるURLを追加する。
基本的にはgenerateオプションのroutesと同じように記述すればOK
上のコードはAPIから記事の一覧を取得して、記事毎のURLをroutesに追加する例。



***
# markdown
1. markdown-itをインストール 
```
$ npm i @nuxtjs/markdownit
```
2. nuxt.configに設定を追記 
```
markdownit: {
    preset: 'default'
    injected: true, 
    breaks: true, 
    html: true, 
    linkify: true,
    typography: true, 
    xhtmlOut: true,
    langPrefix: 'language-',
    quotes: '“”‘’',
    highlight: function (/*str, lang*/) { return ''; },
  },
```
3. $md を使ってパースする場合
オプションのinjected:trueに設定すると、$mdという変数が使えます。
```
<template>
  <div v-html="$md.render(model)"></div>
</template>

<script>
export default {
  data() {
    return {
      model: '# Hello World!'
    }
  }
}
</script>
```
4. .mdファイルを使ってパースする場合
```
<template>
  <div v-html="sample"></div>
</template>

<script>
  import sample from '../sample.md'

  export default {
    computed: {
      sample() {
        return sample
      }
    }
  }
</script>
```
ex:https://techblog.scouter.co.jp/entry/2019/01/24/190000 

# eslintrc.js
## console.logの使用
```
    rules: {
        'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
        'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
    }
```
# layouts
> layouts ディレクトリ関連 
## カスタムレイアウト
1. layouts ディレクトリに新規レイアウト(layouts/topPage.vue)を作成を作成する。 
```
    <template>
    <div class="topPage">
        <HeaderNav />
        <nuxt />
    </div>
    </template>
    <script>
    import HeaderNav from '~/components/header/HeaderNav.vue'
    export default {
    layout: 'topPage',
    components: {
        HeaderNav
    }
    }
    </script>
    <style scoped lang="scss">
    </style>

```
2. ページ (pages/works/index.vue ) で、カスタムレイアウトを使うことを伝えます
```
<script>
export default {
  layout: 'topPage',
}
</script>

```

***
# components
> componentsディレクトリ関連 

***
# page
> pageディレクトリ関連 
## transition プロパティ
1. 特定のページ遷移のトランジション 
```
export default {
  transition: 'content'
}
```
```
//コンテンツ全体をスライド
.content-slide-enter-active, .content-slide-leave-active {
    transition: all 1s;
}
.content-slide-enter, .content-slide-leave-to {
    transform: translateX(100vw) ;
}
```
2. すべてのページ遷移のトランジション 
```
//アプリケーションのすべてのページでフェードさせるトランジション
 .page-enter-active, .page-leave-active {
     transition: opacity .5s;
 }
 .page-enter, .page-leave-to {
     opacity: 0;
 }

```
## head メソッド
1. 個別のページへのHTMLのheadタグを設定する 
```
<script>
export default {
  data() {
    return {
      pageTitle: 'Works Content'
    }
  },
  head() {
    return {
      title: this.pageTitle,
      meta: [
        // `hid` は一意の識別子として使用されます。 `vmid` は動作しないので使わないでください。
        { hid: 'description',
          name: 'Works by Nuxt.js',
          content: 'このページは、Vue.jsフレームワークのNuxt.jsを使って作成したWebサイトを紹介しています。' }
      ]
    }
  },
}
</script>
```
***
# store
> storeディレクトリ関連  
## モジュールモード
`store/index.js`
```
export const state = () => ({
  page: 'home'
})

export const mutations = {

  pagePathSet(state, payload) {
    state.page = payload
  },
}
```
`pages/works/index.vue`
```
<template>
  <div class="container">
    <div class="content-footer">
      <nav class="links">
        <a class="menu_link" @click="link_commit('/works')">
          WORKS
        </a>
        <a class="menu_link" @click="link_commit('/about')">
          ABOUT
        </a>
        <a class="menu_link" @click="link_commit('/contact')">
          CONTACT
        </a>
      </nav>
    </div>
  </div>
</template>
<script>
  computed: {
    page() {
      return this.$store.state.page
    }
  },
  methods: {
    link_commit(linkPath) {
      this.$store.commit('pagePathSet', linkPath)
      setTimeout(() => {
        this.$router.push({ path: linkPath })
      }, 500)
    }
  }
}
</script>
```

# GitHub 
## GitHub リポジトリの作成 
1. GitHub ログイン後のトップページから、Repositories の New ボタンをクリックします。 
2. Create a new repository の画面に遷移するので、リポジトリ名、ライセンス等を入力。Initialize this repository with a READMEはチェックせず画面下のほうにある Create repository ボタンをクリックします。 
 
## プロジェクトを GitHub に Push する 
1. git add -A 
2. git commit -m "first commit" 
3. git remote add origin https://github.com/hiramatsuYoshiaki/プロジェクト名 
4. git push -u origin master 

## 現在のブランチから派生ブランチを作成してGitHubへPushする。  
1. git branch new-branch 
2. git checkout new-branch 
3. git branch 
   * new-branch 
     master 
4. git add -A 
5. git commit -m 'new branch commit' 
6. git push --set-upstream origin new-branch 
   (もしくは、　git push -u origin new-branch) 

## GitHubリポジトリをcloneしてローカルプロジェクト作る 
1. リモートリポジトリをcloneする。 
```
    git clone https://github.com/hiramatsuYoshiaki/vue-cli3-app.git  
```
2. インストールする  
```
    npm install  
```
3. サーバーを立ち上げて確認    
```
   npm run dev
```
4. ローカルサーバーへアクセス 
```
   http://localhost:3000/で確認する。 
```

## ローカルプロジェクトをGitHubへpushする。 
```
1. 現在のブランチを確認する。
   git branch  
   * master  
```
2. masterから新しいbranchを作る  
```
　　git branch new-branch   
```
3. 新しいbranchに移動し開発を行う。 
``` 
   git checkout new-branch  
   ```
4. cloneしたリポジトリから別のリモートリポジトリのURLを変更する場合  
```
    git remote -v
    origin  https://github.com/hiramatsuYoshiaki/vue-cli3-unit.git (fetch)  
    origin  https://github.com/hiramatsuYoshiaki/vue-cli3-unit.git (push)  
    git remote rm originで現在のリモートリポジトリを削除する  
    git remote add originで新しいリモートリポジトリを追加する   
    git remote add origin https://github.com/hiramatsuYoshiaki/vue-cli3-unit-alprime.git
```
5. コミットしてGitHubにpushする  
```
   git add　-A  
   git commit -m "コメント"  
   git push -u origin new-branch  
```  

## localでいままで作業していたbranchを削除する 
  1.これで削除できます。これはしなくてもいいですが、開発が進んでいくとbranchが増えてbranch一覧がごちゃごちゃしてくるのでやったほうがいいです。  
  ```
  git branch -d new-branch  
  ```

## 他の人の開発分を取り込む 
1. masterに他の人が追加した分を自分のところに取り込みます。 
```
  git pull origin master  
```

# netlify 
1. netlifyログインする。 
2. 画面右上の「New site from Git」を押す。 
3. 「Github」を押す。 
4. リポジトリを選択する。 
```
  next-univ-app1
```
5. ブランチを選択し「Deploy site」ボタンを押す。 
```
  branch to deploy : master
```
6. ビルドコマンドを入力する。 
```
  build comand : nuxt generate
```
6. ジェネレート先のディレクトリがどこなのかを指定します。 
```
  publish directory : dist
```
6. ビルドコマンドを入力する。 
```
  build comand : nuxt generate
```
## 他の人の開発分を取り込む 
1. masterに他の人が追加した分を自分のところに取り込みます。 
```
  git pull origin master  
```
## Githubへのpushでusername/passwordの入力対応（https）
https://did2memo.net/2015/07/26/github-remember-username-https/
https://garicchi.com/?p=19323
#usernameの入力省略
1. リモートリポジトリの接続を確認する
```
$ git remote -v
origin  https://github.com/hiramatsuYoshiaki/nuxt-univ-firebase-app2.git (fetch)
origin  https://github.com/hiramatsuYoshiaki/nuxt-univ-firebase-app2.git (push)
```
clone時にhttpsのurlでcloneしたのでhttps通信方法になっている。 
 
2. リモートリポジトリを削除する。
```
$ git remote rm
```
3. リモートリポジトリのurlにユザー名入れて追加する。
```
$ git remote add origin https://hiramatsuYoshiaki@github.com/hiramatsuYoshiaki/nuxt-univ-firebase-app2.git
```
push時にユザー名は聞かれない。 
 
#usernameの入力省略
https://help.github.com/en/articles/caching-your-github-password-in-git
1. パスワードを一定時間保持して、入力を省略する。
Windows を使っているなら、wincred という補助ツールがあります。 
Windows Credential Store）で、重要な情報を管理します。 
```
$ git config --global credential.helper wincred 
```
15分パスワードを保持
```
$ git config --global credential.helper wincred cache 'cache --timeout=3600'
```
60分パスワードを保持