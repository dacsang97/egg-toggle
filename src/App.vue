<template>
  <div>
    <a href="https://github.com/dacsang97/egg-toggle">
      <octocat></octocat>
    </a>
    <div id="app">
      <div id="egg-toggle" ref="egg" @click="onClicked"></div>
    </div>
  </div>
</template>

<script>
import Octocat from './Octocat.vue'
import eggFlip from './assets/egg_flip.json'

export default {
  name: 'app',
  components: {
    Octocat
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      anim: null
    }
  },
  mounted () {
    this.anim = bodymovin.loadAnimation({
        wrapper: this.$refs.egg,
        animType: 'svg',
        loop: false,
        prerender: false,
        autoplay: false,
        animationData: eggFlip
      });
    this.anim.setSpeed(15);
  },
  methods: {
    onClicked () {
      if (this.anim.currentFrame > 0) {
        this.anim.playSegments([this.anim.currentFrame, 0], true);
        TweenMax.to('.eggGroup', 1, {
          x:0,
          ease:Elastic.easeOut.config(0.9,0.38)
        })   
      } else {
        TweenMax.to('.eggGroup', 1.4, {
          x:73,
          ease:Elastic.easeOut.config(0.9,0.38)
        })
        this.anim.playSegments([this.anim.currentFrame, 300], true)
      }
    }
  }
}
</script>

<style lang="scss">
body, #app {
 background-color: #29AFB0;
 overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

body,
html {
 height: 100%;
 width: 100%;
 margin: 0;
 padding: 0;
}

#egg-toggle {
 width: 50%;;
 height: 50%;
 -webkit-tap-highlight-color:transparent;

 cursor:pointer;
}
</style>
