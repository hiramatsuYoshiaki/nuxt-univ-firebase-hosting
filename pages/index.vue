<template>
  <div class="container">
    <div class="content-header">
      <logo />
      <h1 class="title">
        h-works
      </h1>
      <h2 class="subtitle">
        Nuxt.js Universal SSR
      </h2>
      <h2 class="subtitle">
        Circle CI with Docker + Firebase
      </h2>
      <p class="subtitle">
        Nuxt-univ-firebase-hosting
      </p>
      <p class="subtitle">
        NuxtアプリケーションをCircleCIでFirebaseに自動ディプロイ
      </p>
    </div>

    <transition name="mainCon" appear>
      <div class="content-logo-section">
        <img src="~assets/img/logo/circleci.png" alt="circle ci logo">
        <!-- <img src="~assets/img/logo/docker2.png" alt="circle ci logo"> -->
        <!-- <img src="~assets/img/logo/firebase.png" alt="circle ci logo"> -->
      </div>
    </transition>
    <div class="content">
      <section>
        <a class="github sec-link" href="https://github.com/hiramatsuYoshiaki/nuxt-univ-firebase-hosting">
          <h3>GitHub</h3>
          <div class="word-wrap">Repository</div>
          <div class="word-wrap">https://github.com/hiramatsuYoshiaki/nuxt-univ-firebase-hosting</div>
        </a>
      </section>
      <section>
        <a class="netlify sec-link" href="https://nuxt-app2.firebaseapp.com/">
          <h3>Firebase </h3>
          <div class="word-wrap">Hosting</div>
          <div class="word-wrap">https://nuxt-app2.firebaseapp.com/</div>
        </a>
      </section>
    </div>
    <transition name="mainCon" appear>
      <div class="content-footer">
        <ContentFooter />
      </div>
    </transition>

    <transition appear name="transitionScreen">
      <TransitionScreen v-if="page === '/'" />
    </transition>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import TransitionScreen from '~/components/transition/TransitionScreen.vue'
import ContentFooter from '~/components/content/ContentFooter.vue'

export default {
  layout: 'topPage',
  // transition: 'content-slide',
  components: {
    Logo,
    ContentFooter,
    TransitionScreen
  },
  data() {
    return {
      img: require('~/assets/img/img1578.jpg'),
      pageTitle: 'Landing Content',
      pageSubTitle: 'Nuxt.js Demo Site',
      pageDiscription: 'Landing',
      pageDiscriptionDetail: 'Vue.jsのフレームワークNuxt.jsを使ったデモサイトです。'
    }
  },
  head() {
    return {
      title: this.pageTitle,
      meta: [
        { hid: 'description',
          name: 'landing by Nuxt.js',
          content: 'このページは、Vue.jsフレームワークのNuxt.jsを使って作成したデモサイトです。' }
      ]
    }
  },
  computed: {
    page() {
      return this.$store.state.page
    }
  }
}
</script>

<style scoped lang="scss">
%center{
    display:flex;
    justify-content: center;
    align-items: center;
}
%left{
    display:flex;
    justify-content: flex-start;
    align-items: center;
}
%right{
    display:flex;
    justify-content: flex-end;
    align-items: center;
}
.container{
  margin-top: $header-height;
  width: 100vw;
  padding: 2rem;
  @media (min-width: 992px){
    padding: 5rem;
  }
  @extend %center;
  flex-direction: column;
}
//header-----------------------------
.content-header{
  @extend %center;
  flex-direction: column;
}
//content -----------------------
.content{
  margin-top:4rem;
  display:flex;
  flex-direction: column;
  width: 100%;
  @media(min-width: 992px){
    width: 80%;
    display:flex;
    justify-content: flex-start;
    align-items: flex-start;
    flex-direction: row;
  }
}
section{
  width: 100%;
  margin-top:2rem;
  padding: 2rem;
  @media(min-width: 992px){
    width: 50%;
    .github{
      text-align: right;
      margin-bottom: 2rem;
      display: block;
    }
    .netlify{
       margin-bottom: 2rem;
       display: block;
    }
  }

}
.links{
  @extend %center;
}
.links a{
  display: inline-block;
  margin: 0 2rem;
  cursor: pointer;
}
.word-wrap{
  word-wrap: break-word;
}
.title{
  margin-top:2rem;
}
// footer-------------------------------
// .content-footer{
//   width: 100%;
//   margin-top:4rem;
//   @extend %center;
//   flex-direction: column;
// }
// .content-footer nav{
//   margin-top: 2rem;
// }
// .footer-sepalater{
//  width: 100%;
//  height: 2rem;
//  display: flex;
//  justify-content: center;
//  align-items: center;
// }
// .footer-sepalater .line{
//   width:80%;
//   height: 1px;
//   background-color: #fff;
// }
.content-logo-section{
  width: 100vw;
  height: 30rem;
  display:flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-bottom: -5rem;
  background-color: #fff;
  margin-top:4rem;
  padding: 2rem 0;
  @extend %center;
  flex-direction: column;
  img{
    width: 80%;
    height: auto;
  }
  @media(min-width: 992px){
    img{
    width: 20%;
    height: auto;
  }
  }
}
.content-footer{
  width: 100vw;
  display:flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-bottom: -5rem;
}

</style>
