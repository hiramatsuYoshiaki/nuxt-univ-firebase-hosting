<template>
  <div class="worksIntro">
    <h1>Overview</h1>
    <p>
      Vue.jsのフレームワークNuxt.jsを使ったデモサイトです。
      このウェブアプリケーションは、GithubとCircleCIに連携しています。
      Githubのブランチにマージすると、
      CircleCIが自動的でアプリケーションをFirebaseに自動デプロイします。。
    </p>

    <div class="flex-container select-mode">
      <div class="two-col">
        <section>
          <div class="mode-text">
            GitHub + CircleCI
          </div>
          <h5>自動ディプロイ</h5>
        </section>
        <section>
          <h3>継続的インテグレーションとは</h3>
          <p>
            プログラマーのアプリケーション作成時の品質改善や納期の短縮のためプロセスを自動化すること、具体的には、ビルドやテストなどを継続的に実行していくことで、
            開発者がソースコードをコミットし、共有しているリポジトリにマージされることでビルドとテストが自動的に実行される手法です。
            継続的インテグレーションを導入する事により、ソフトウェアのバグを効率的に発見でき、開発者の負担を軽減しながら開発スピードと,コードの品質を向上することが可能です。
          </p>
        </section>

        <section>
          <h3>メリット</h3>
          <ul>
            <li><p>バグを短時間で発見し、対処することが可能</p></li>
            <li><p>チームの生産性と効率アップ</p></li>
            <li><p>品質の高い、安定した製品のリリース</p></li>
          </ul>
        </section>
        <section>
          <div class="mode-text">
            Docker
          </div>
          <h5>ビルド環境</h5>
        </section>
        <section>
          <h3>Dockerとは</h3>
          <p>Dockerは、開発者やシステム管理者がコンテナを使用してアプリケーションを開発、デプロイ、および実行するためのプラットフォームです。</p>
        </section>
        <section>
          <h3>Docker </h3>
          <p>
            CircleCI 2.0はDockerエグゼキュータを使用してビルドサポートを実装します。
            エグゼキュータは、CI / CDジョブ/設定がCircleCIプラットフォーム内で実行される環境です。
            Dockerエグゼキュータの設定は、config.ymlビルド構成ファイル内で定義されています。
          </p>
        </section>
      </div>
      <div class="two-col">
        <section>
          <div class="mode-text">
            Docker Executors
          </div>
          <h5>Dockerエグゼキュータの設定</h5>
        </section>
        <section>
          <h3>Dockerエグゼキュータの設定(config.yml)</h3>
          <p>
            CircleCIジョブは、ビルドするために、Dockerエグゼキュータの使用法をconfig.ymlに指定します。
          </p>
        </section>
        <section>
          <h3>config.yml</h3>
          <div v-html="$md.render(config)" />
        </section>
        <section>
          <h3>config.ymlの補足説明</h3>
          <p><span class="key-bold">version: </span>は、2、2.0、2.1 のうちのどれかを指定します。</p>
          <p><span class="key-bold">jobs: </span>は、Workflows を利用する際は、ユニークなジョブ名（deploy_dev）を付けます。</p>
          <p><span class="key-bold">docker: </span>は、docker Executorを使用します。imageには、使用するカスタム Docker イメージの名前を指定します。ローカルの実行環境と同じにします。（node:10.15.3） </p>
          <p><span class="key-bold">steps: </span>は、ジョブにおける steps の設定は、キーと値のペアを 1 つずつ列挙する形で行います。 </p>
          <p><span class="key-bold">checkout: </span>は、設定済み path（デフォルトは working_directory）にあるソースコードのチェックアウトに用いる特殊なステップです。単純に checkout する場合は、ステップタイプは属性なしで文字列を記述するだけです。 path が存在し、かつソースコードが git リポジトリの場合は、ステップはリポジトリ全体をクローンせず、オリジナルをプルします。同様の条件で git リポジトリ以外の場合は、このステップは失敗します。 </p>
          <p><span class="key-bold">run: </span>は、ステップのタイプとなります。 name 属性は CircleCI 上での表示に使われるものです。command 属性は run ステップに特有の、実行するコマンドを定義するものです。</p>
          <p><span class="key-bold">workflows: </span>は、あらゆるジョブの自動化に用います。Workflow 1 つ 1 つはそれぞれ名前となるキーと、値となるマップからなります。 </p>
          <p><span class="key-bold">filters: </span>は、は、trigger を定義した config.yml ファイルを含むブランチにおいて、スケジュール実行すべきブランチかどうかを決定するのに使えます。つまり、master ブランチにプッシュすると、master ブランチの Workflows のみをスケジュール実行します。branches では、ブランチ名を指す文字列をマップさせるための only キーが使えます。only の値にマッチするブランチはすべてジョブを実行します。 </p>
        </section>
      </div>
    </div>
  </div>
</template>
<script>

export default {
//   props: {
//     pageTitle: {
//       type: String,
//       default: 'a'
//     },
//   }
  data() {
    return {
      config: `
    version: 2
    jobs:
      deploy_dev: # ジョブ名
        docker:
          - image: circleci/node:10.15.3 # ジョブ実行環境のDockerイメージを記述
        steps:
          - checkout # ソースコードのチェックアウト
          - run:
              name: Add env # .envを作成、セキュリティためGitHubにはアップしないため
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
  }
//   computed: {
//     page() {
//       return this.$store.state.page
//     }
//   },
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
.worksIntro{
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  padding: 2rem 2rem;
  @media (min-width: 768px) {
      padding: 8rem 8rem;
  };
  border: 1px solid  rgba(0,0,0,.2);
}
.flex-container{
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  @media (min-width: 768px) {
      flex-direction: row;
  };
}
.select-mode{
    margin-top:2rem;
}
.two-col{
    width: 100%;
    @media (min-width: 768px) {
        width: 50%;
        padding-right: 8rem;
    };
    padding-right: 2rem;
    padding-bottom: 2rem;
    section{
      margin-bottom: 2rem;
    }
    h3{
      color:#000000;
      font-weight: 600;
      margin-bottom:2rem;
    }
    p{
      color:rgb(70, 69, 69);
    }
}
.mode-text{
    font-size: 4rem;
    font-weight: 700;
    color: green;
    @media (min-width: 768px) {
        font-size: 8rem;
    };
}
a{
    color: black;
}
.word-wrap{
    word-break: break-all;
}
li{
  margin-bottom:2rem;
}
p{
  word-wrap: break-word;
  font-size: 1.6rem;
  @media (min-width: 768px) {
        font-size: 2rem;
    };
}
.key-bold{
  font-weight: 600;
  color: rgb(16, 98, 3);
}
</style>
