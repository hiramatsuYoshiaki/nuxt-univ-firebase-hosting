<template>
  <div class="aboutIntro">
    <div class="flex-container">
      <div class="side-col">
        <p>Demoの使い方</p>
        <div v-for="(mdData, index) in mdDatas" :key="index">
          <p
            class="topMenu "
            :class="{ activeTopMenu : selectMenu === index}"
            @click="menuActive(index)"
          >
            {{ mdData.topMenu }}
          </p>
          <div v-if="selectMenu === index">
            <div v-for="(usage, index) in mdData.usages" :key="index">
              <div class="subMneu">
                {{ usage.subMenu }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="main-col">
        <div v-for="(mdData, index) in mdDatas" :key="index">
          <div class="topMain h1-res">
            {{ mdData.topMenu }}
          </div>

          <div v-for="(usage, index) in mdData.usages" :key="index">
            <div class="subMainTitle">
              <div class="h3-res">
                {{ usage.title }}
              </div>
            </div>
            <div class="subMainDescription">
              <p>{{ usage.Description }}</p>
            </div>

            <div v-for="(operation, index) in usage.operations" :key="index">
              <div class="subMainOperation">
                {{ index + 1 }}.  {{ operation.opeTitle }}
              </div>
              <div class="subMainComandWrap">
                <div v-for="(comand, index) in operation.comands" :key="index">
                  <div class="subMainComand">
                    <div v-html="$md.render(comand.cmd)" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- <div v-html="$md.render(model)" /> -->
        <!-- <div v-html="$md.render(model2)" />
        <div v-html="readMe" /> -->
      </div>
    </div>
  </div>
  </div>
</template>
<script>
// import readMe from '~/assets/readMe/readMe.md'
// import TransitionScreen from '~/components/transition/TransitionScreen.vue'

//       img: require('~/assets/img/img3668.jpg'),
export default {
//   props: {
//     pageTitle: {
//       type: String,
//       default: 'a'
//     },
//   }
  data() {
    return {
    //   model: `# Hello World!`,
    //   model2: `# nuxt.js!`,
      selectMenu: null,
      //   isActiveMenu: [],
      //   isActive: false,

      mdDatas: [
        {
          topMenu: `１．プロジェクトを作るa`,
          topMenuMd: `１．プロジェクトを作るb`,
          usages: [
            {
              subMenuId: 1,
              subMenu: 'ローカルプロジェクトを作るc',
              title: 'GitHubリポジトリをcloneしてローカルプロジェクト作る。d',
              Description: 'hiramatsuYoshiaki/nuxt-univ-app2リポジトリをベースにして、ローカルプロジェクトを新規作成して開発を開始します。e',
              operations: [
                {
                  opeTitle: '新規ローカルプロジェクトのディレクトリを作成する',
                  comands: [
                    {
                      cmd: '    $ md new-project'
                    }
                  ]
                },
                {
                  opeTitle: 'リモートリポジトリをcloneする。',
                  comands: [
                    {
                      cmd: '    $ git clone https://github.com/hiramatsuYoshiaki/nuxt-univ-app2.git'
                    }
                  ]
                },
                {
                  opeTitle: ' サーバーを立ち上げて確認',
                  comands: [
                    {
                      cmd: '    $ npm run dev'
                    }
                  ]
                },
                {
                  opeTitle: 'インストールする',
                  comands: [
                    {
                      cmd: '    $ npm install'
                    }
                  ]
                },
                {
                  opeTitle: 'サーバーを立ち上げて確認',
                  comands: [
                    {
                      cmd: '    $ npm run dev'
                    }
                  ]
                },
                {
                  opeTitle: 'ローカルサーバーへアクセス',
                  comands: [
                    {
                      cmd: '    http://localhost:3000/で確認する。'
                    }
                  ]
                }
              ]
            },
            {
              subMenuId: 2,
              subMenu: 'リモートプロジェクトを作成する。ｃ',
              title: ' GitHub リポジトリの作成',
              Description: '新規プロジェクト用のリポジトリを作り、チーム開発のバージョン管理を行います。',
              operations: [
                {
                  opeTitle: 'GitHub ログイン後のトップページから、Repositories の New ボタンをクリックします。',
                  comands: [
                    {
                      cmd: `    「NEW」または、「Start a project」ボタンを押す。`
                    }
                  ]
                },
                {
                  opeTitle: 'Create a new repository の画面に遷移するので、リポジトリ名、簡単な説明を入力する。',
                  comands: [
                    {
                      cmd: `    Repository name: リポジトリ名`
                    },
                    {
                      cmd: '    Description: 簡単な説明'
                    },
                    {
                      cmd: '    publicにチェックを入れる'
                    },
                    {
                      cmd: '    Initialize this repository with a READMEはチェックせず画面下のほうにある 「Create repository」 ボタンをクリックします。'
                    }
                  ]
                },
                {
                  opeTitle: 'プロジェクトを GitHub に Push する',
                  comands: [
                    {
                      cmd: '    git add .'
                    },
                    {
                      cmd: '    git commit -m "first commit"'
                    },
                    {
                      cmd: '    git remote add origin https://github.com/リポジトリ名/プロジェクト名'
                    },
                    {
                      cmd: '    git push -u origin master'
                    }
                  ]
                },
                {
                  opeTitle: 'ローカルプロジェクトで現在のブランチから開発用の派生ブランチ(dev)を作成してGitHubへPushする。',
                  comands: [
                    {
                      cmd: '    git branch new-branch(dev)'
                    },
                    {
                      cmd: '    git checkout new-branch(dev)'
                    },
                    {
                      cmd: '    git add -A '
                    },
                    {
                      cmd: '    git commit -m "new branch dev commit"'
                    },
                    {
                      cmd: '    git push --set-upstream origin dev'
                    }
                  ]
                },
                {
                  opeTitle: 'GitHubでDevブランチをmasterブランチにマージする。',
                  comands: [
                    {
                      cmd: '    codeタグを選択し、branch:masterボタンを押し、開発用のブランチ（dev）を選択する。'
                    },
                    {
                      cmd: '    New pull requestボタンを押す'
                    },
                    {
                      cmd: '    Create pull requestボタンを押す '
                    },
                    {
                      cmd: '    Confirm margeボタンを押す'
                    },
                    {
                      cmd: '    Delete branchボタンを押す'
                    }
                  ]
                }
              ]
            }
          ]
        },

        {
          topMenu: `２．ホスティングする。`,
          topMenuMd: `２．ホスティングする。`,
          usages: [
            {
              subMenuId: 1,
              subMenu: 'Firebaseへホスティングする。',
              title: ' Firebaseで新規プロジェクトを作成しディプロイする。',
              Description: 'Firebaseで新規プロジェクトを作成した後に、プロジェクトをFirebaseにホスティングします。',
              operations: [
                {
                  opeTitle: 'Firebaseのコンソール画面から、新規プロジェクトの作成ボタンを押し、プロジェクト名を入力し、プロジェクト作成ボタンを押します。',
                  comands: [
                    {
                      cmd: '    「プロジェクト作成」を押す。'
                    }
                  ]
                },
                {
                  opeTitle: 'Firebase CLI をインストール',
                  comands: [
                    {
                      cmd: '    $ npm install -g firebase-tools'
                    }
                  ]
                },
                {
                  opeTitle: ' Firebase プロジェクトにアクセスする',
                  comands: [
                    {
                      cmd: '    $ firebase login'
                    }
                  ]
                },
                {
                  opeTitle: ' サイトを初期化する（firebasercとfirebase.jsonを作る）',
                  comands: [
                    {
                      cmd: '    $ firebase init'
                    },
                    {
                      cmd: '    ? Are you ready to proceed?'
                    },
                    {
                      cmd: '    ⇒　yを押して、enterを押す'
                    },
                    {
                      cmd: '    ? Which Firebase CLI features do you want to set up for this folder?'
                    },
                    {
                      cmd: '      Press Space to select features, '
                    },
                    {
                      cmd: '      then Enter to confirm your choices. Hosting:'
                    },
                    {
                      cmd: '      Configure and deploy Firebase Hosting sites'
                    },
                    {
                      cmd: '    ⇒ 下矢印キーを押してリストからhostingを選択し、'
                    },
                    {
                      cmd: '       スペースキーを押して、enterを押す。(ホスティングのみ選択)'
                    },
                    {
                      cmd: '    ? Select a default Firebase project for this directory:'
                    },
                    {
                      cmd: '    ⇒　下矢印キーを押してリストを選択,'
                    },
                    {
                      cmd: '        スペースキーを押してプロジェクトを選択して。enterを押す'
                    },
                    {
                      cmd: '    ? What do you want to use as your public directory?'
                    },
                    {
                      cmd: '    ⇒　distを入力し、enterを押す'
                    },
                    {
                      cmd: '    ? Configure as a single-page app (rewrite all urls to /index.html)?'
                    },
                    {
                      cmd: '    ⇒　nを入力し、enterを押す。'
                    },
                    {
                      cmd: '    ? File dist/index.html already exists. Overwrite?'
                    },
                    {
                      cmd: '    ⇒　nを入力し、enterを押す。'
                    }
                  ]
                },
                {
                  opeTitle: ' アプリケーションのルートディレクトリにfirebasercとfirebase.jsonができていることを確認する。',
                  comands: [
                    {
                      cmd: '    firebaserc '
                    },
                    {
                      cmd: '    firebase.json'
                    }
                  ]
                },
                {
                  opeTitle: ' buildもしくは、generateする',
                  comands: [
                    {
                      cmd: '    $ npm run build もしくは、npm run generate'
                    }
                  ]
                },
                {
                  opeTitle: ' ローカルで実行してテストしてみる',
                  comands: [
                    {
                      cmd: '    $ firebase serve'
                    },
                    {
                      cmd: '    localhost:5000/にアクセスして確認する'
                    }
                  ]
                },
                {
                  opeTitle: ' firebaseにディプロイする',
                  comands: [
                    {
                      cmd: '    $ firebase deploy'
                    }
                  ]
                },
                {
                  opeTitle: ' firebaseにホスティングされていることを確認する。',
                  comands: [
                    {
                      cmd: '    https://nuxt-app-xxxx.firebaseapp.com/にアクセス、'
                    },
                    {
                      cmd: '    または、firebaseのダッシュボードからアクセスして確認する。'
                    }
                  ]
                }
              ]
            }

          ]
        },
        { topMenu: `３．自動ディプロイ`,
          topMenuMd: `３．自動ディプロイ`,
          usages: [
            {
              subMenuId: 1,
              subMenu: 'Circle CIの設定a',
              title: ' Circle CIで自動ビルド設定する。',
              Description: 'GitHubのDevブランチへpushしたら、Circle CIでFirebaseへ自動でディプロイする',
              operations: [
                {
                  opeTitle: 'プロジェクトで以下のコマンドを実行し、デプロイ用のFirebaseトークンを取得する。表示されたデプロイ用のFirebaseトークンはコピーしておく。',
                  comands: [
                    {
                      cmd: `     $ firebase login:ci                     `
                    }
                  ]
                },
                {
                  opeTitle: 'CircleCIにログイン後、画面のサイドバーから「SETTINGS」を選択し、「projects」クリックしてGitHubリポジトリのリストを表示する。',
                  comands: [
                    {
                      cmd: `     settingをクリックし、次にprojectをクリック                     `
                    }
                  ]
                },
                {
                  opeTitle: ' 該当するリポジトリの右端にある、歯車アイコンをクリックする。',
                  comands: [
                    {
                      cmd: '    歯車アイコンをクリック'
                    }
                  ]
                },
                {
                  opeTitle: ' BUILD SETTINGSの「Environment Variables」をクリックし、画面遷移する。',
                  comands: [
                    {
                      cmd: '    「Environment Variables」をクリック'
                    }
                  ]
                },
                {
                  opeTitle: ' 「Add Variable」ボタンを押し,ポップアップ画面でfirebaseトークンを設定する',
                  comands: [
                    {
                      cmd: '    nema:  FIREBASE_TOKEN'
                    },
                    {
                      cmd: '    value: xxxaoxnMhPCgF8SoK2ND6HDdh4G0-bKm-xxxxxxxxxxxx'
                    }
                  ]
                },
                {
                  opeTitle: ' 「Add Variable」ボタンを押し,ポップアップ画面でfirebaseプロジェクトIDを設定する',
                  comands: [
                    {
                      cmd: '    name:  FIREBASE_PROJECT_ID'
                    },
                    {
                      cmd: '    value: nuxt-app-xxxxxxxx'
                    }
                  ]
                },
                {
                  opeTitle: ' 「Add Variable」ボタンを押し,ポップアップ画面でfirebaseConfigを設定する',
                  comands: [
                    {
                      cmd: '    name:  FIREBASE_API_KEY'
                    },
                    {
                      cmd: '    value: xxxxxxxxx_zE8_oNkN43OS-xhlIIAQv2uOjLTLI'
                    }
                  ]
                },
                {
                  opeTitle: ' 「Add Variable」ボタンを押し,ポップアップ画面でfirebaseホスティングドメインを設定する',
                  comands: [
                    {
                      cmd: '    name:  FIREBASE_AUTH_DOMAIN'
                    },
                    {
                      cmd: '    value: nuxt-app-xxxx.firebaseapp.com'
                    }
                  ]
                },
                {
                  opeTitle: ' 「Add Variable」ボタンを押し,ポップアップ画面でfirebaseデータベースURLを設定する',
                  comands: [
                    {
                      cmd: '    name:  FIREBASE_DATABASEURL'
                    },
                    {
                      cmd: '    value: https://nuxt-app-xxxx.firebaseio.com'
                    }
                  ]
                },
                {
                  opeTitle: ' 「Add Variable」ボタンを押し,ポップアップ画面でfirebaseプリジェクトIDを設定する',
                  comands: [
                    {
                      cmd: '    name:  FIREBASE_PROJECTID'
                    },
                    {
                      cmd: '    value: nuxt-app-xxxx'
                    }
                  ]
                },
                {
                  opeTitle: ' 「Add Variable」ボタンを押し,ポップアップ画面でfirebaseストレージバケットを設定する',
                  comands: [
                    {
                      cmd: '    name:  FIREBASE_STORAGEBUCKET'
                    },
                    {
                      cmd: '    value: nuxt-app-xxxx.appspot.com'
                    }
                  ]
                }
              ]
            },
            {
              subMenuId: 2,
              subMenu: '環境変数を設定b',
              title: ' dotenvを使う',
              Description: 'dotenv を使って.envファイルに設定した環境変数をFirebaseのconfigで使う',
              operations: [
                {
                  opeTitle: 'dotenvをインストールをインストールする。',
                  comands: [
                    {
                      cmd: `    $ npm i @nuxtjs/dotenv             `
                    }
                  ]
                },
                {
                  opeTitle: 'nuxt.config.jsを編集する',
                  comands: [
                    {
                      cmd: `
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
                      `
                    }
                  ]
                },
                {
                  opeTitle: ' .envをルートディレクトリに作りキーを設定する。',
                  comands: [
                    {
                      cmd: `
    FIREBASE_API_KEY='<key>'
    FIREBASE_AUTH_DOMAIN='oauth3.firebaseapp.com'
    FIREBASE_DATABASEURL='https://oauth3.firebaseio.com'
    FIREBASE_PROJECTID='oauth3'
    FIREBASE_STORAGEBUCKET='oauth3.appspot.com'
                      `
                    }
                  ]
                },
                {
                  opeTitle: ' Firebase configにprocess.envを使って設定をする。',
                  comands: [
                    {
                      cmd: `
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
                      `
                    }
                  ]
                }
              ]
            },
            // eslintのフォーマットエラーの解消
            {
              subMenuId: 3,
              subMenu: 'Dockerイメージ',
              title: ' Dockerイメージ',
              Description: 'Dockerイメージをconfig.ymlに作りCircleCIに自動ディプロイさせる',
              operations: [
                {
                  opeTitle: ' CircleCIではnpm -gでのコマンド実行が出来ないため、グローバルインストールのみの場合は、pakage.jsonに追加するために、プロジェクトにインストールする。',
                  comands: [
                    {
                      cmd: `    $ npm install --save-dev firebase-tools                  `
                    },
                    {
                      cmd: `    $ npm install --save-dev @nuxtjs/dotenv                  `
                    }
                  ]
                },
                {
                  opeTitle: ' CircleCIの設定ファイルを作成。プロジェクト直下に`.circleci/config.yml`ファイルを作成ます。(ファイル名の先頭に.を付ける点に注意)',
                  comands: [
                    {
                      cmd: `    .circleci/config.yml                  `
                    }
                  ]
                },
                {
                  opeTitle: ' .circleci/config.ymlを編集する',
                  comands: [
                    {
                      cmd: `
    version: 2
    jobs:
      deploy_dev: # ジョブ名
        docker:
          - image: circleci/node:10.15.3 # ジョブ実行環境のDockerイメージを記述
        steps:
          - checkout # ソースコードのチェックアウト
          - run:
              name: Add env # .envを作成セキュリティためGitHubにはアップしないため
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
              command: ./node_modules/.bin/firebase deploy --project=$FIREBASE_PROJECT_ID --token=$FIREBASE_TOKEN 
              # プロジェクト上のfirebase-toolsでデプロイします

    workflows:
      version: 2
      deploy_dev: # ワークフローの名前
        jobs:
          - deploy_dev: # 上で定義したジョブを指定します
              filters:
                branches:
                  only: dev # developブランチのみを実行対象とします。今回はdevブランチ                      
                      `
                    }
                  ]
                }
              ]
            }

          ]
        }
      ]
    }
  },
  //   computed: {
  // page() {
  //   return this.$store.state.page
  // }

  // readMe() {
  //   return readMe
  // }

  //   },
  methods: {
    menuActive(index) {
      if (this.selectMenu === index) {
        this.selectMenu = null
        // this.isActiveMenu[index] = false
      } else {
        this.selectMenu = index
        // this.isActiveMenu[index] = true
      }
    }
  }
//   created: function () {
//     this.isMenu = false
//   }
//   methods: {
//     link_commit(linkPath) {
//       this.active = true
//       this.$store.commit('pagePathSet', linkPath)
//       setTimeout(() => {
//         this.$router.push({ path: linkPath })
//       }, 500)
//     }
//   }
}
</script>
<style scoped lang="scss">
.aboutIntro{
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  padding: 2rem 2rem;
//   @media (min-width: 992px) {
//       padding: 8rem 8rem;
//   };
//   border: 1px solid  rgba(0,0,0,.2);
}
.flex-container{
  width: 100%;
  display: flex;
//   flex-direction: column;
  flex-direction: row;
  justify-content: center;
  align-items: flex-start;
//   @media (min-width: 768px) {
//       flex-direction: row;
//   };
}
.side-col{
    width: 100%;
    display: none;
    @media (min-width: 992px) {
        width: 30%;
        display: block;
        padding-right: 10rem;
    };
    // padding-right: 8rem;
    // padding-bottom: 2rem;
    padding: 2rem;
    section{
      margin-bottom: 2rem;
    }
    // h3{
    //   color:#000000;
    //   font-weight: 600;
    // }
    p{
      color:rgb(70, 69, 69);
    }
    // border: 1px solid  rgba(0,0,0,.2);

}
.main-col{
    width: 100%;
    @media (min-width: 992px) {
        width: 70%;
        padding-right: 10rem;
        padding: 2rem;
    };
    section{
      margin-bottom: 2rem;
    }
    // p{
    //   color:rgb(70, 69, 69);
    // }

}
.topMenu{
    color:rgb(70, 69, 69);
    font-weight: 500;
    cursor: pointer;
    padding:0.5rem ;
}

.activeTopMenu{
    background-color: lightgreen;
    border-radius: 2px;
    color: red;
}
.subMneu{
    padding-left: 1.5rem;
}

.topMain{
    border-bottom: 1px solid green;
    margin: 6rem 2rem 2rem 0;

}

.subMainTitle{
    margin: 2rem 2rem 2rem 2rem;
    @media (min-width: 992px) {
        margin: 6rem 2rem 2rem 2rem;
    };

}
.subMainDescription{
    // p{
    //     color: gray;
    // }
    margin: 2rem 2rem 2rem 2rem;
}
.subMainOperation{
    // p{
    //     color: gray;
    // }
    margin: 2rem 2rem 2rem 2rem;
}
.subMainComandWrap{
    background-color: rgb(150, 159, 165);
    padding: 1rem;
    border-radius: 2px;
    font-size: 1rem;
}
.subMainComand{
    font-size: 1.6rem;
    line-height: 2rem;
}
.h1-res{
    color: rgb(5, 121, 5);
    font-weight:700;
    font-size: 2rem;
    @media (min-width: 992px) {
        font-size: 4rem;
    };
}
.h3-res{
    color: rgb(53, 53, 53);
    font-weight:700;
    font-size: 2rem;
    @media (min-width: 992px) {
        font-size: 4rem;
    };
}
p{
    color:rgb(70, 69, 69);
}

</style>
