<template>
  <transition
    @before-enter="beforeEnter"
    @enter="enter"
    :css="false"
    mode="out-in"
  >
    <div v-if="menuOpened" class="menudrawer">
      <nuxt-link exact to="/"><li>Home</li></nuxt-link><br />
      <nuxt-link to="/about"><li>About</li></nuxt-link><br />
      <nuxt-link to="/users"><li>Users</li></nuxt-link><br />
      <nuxt-link to="/contactus"><li>Contact Us</li></nuxt-link>
    </div>
  </transition>
</template>

<script>
// import { mapGetters } from 'vuex'
// import { TweenMax, TimelineMax, Sine, Expo } from 'gsap'
import { TweenMax, Sine } from 'gsap'

export default {
  filters: {
    firstName(input) {
      const lastIndex = input.lastIndexOf(' ')
      return input.substring(0, lastIndex)
    }
  },
  props: {
    menuOpened: {
      type: Boolean,
      default: false
    }
  },
  // computed: {
  //   ...mapGetters(['selectedUser'])
  // },
  methods: {
    beforeEnter(el) {
      TweenMax.set(el, {
        opacity: 0,
        scale: 0,
        transformOrigin: '100% 0%'
      })
      TweenMax.set(el.childNodes, {
        opacity: 0
      })
    },
    enter(el, done) {
      TweenMax.fromTo(
        el,
        0.2,
        {
          opacity: 0,
          scale: 0
        },
        {
          opacity: 1,
          scale: 1,
          ease: Sine.easeOut
        }
      )
      TweenMax.staggerFromTo(
        el.childNodes,
        0.45,
        {
          opacity: 0
        },
        {
          delay: 0.1,
          opacity: 1,
          ease: Sine.easeOut
        },
        0.04
      )
      done()
    }
  }
}
</script>

<style scoped>
.menudrawer {
  background: rgba(0, 0, 0, 0.8);
  line-height: 1.8;
  text-align: right;
  position: absolute;
  right: 0px;
  top: 45px;
  padding: 20px;
  border-radius: 4px;
  z-index: 10000;
}

a,
a:visited,
a:active {
  color: white;
}
</style>
