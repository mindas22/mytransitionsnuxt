<template>
  <div>
    <app-navigation />
    <svg
      :class="{ active: page === 'about' }"
      xmlns="http://www.w3.org/2000/svg"
      width="200"
      height="200"
      viewBox="0 0 447 442"
    >
      <!-- we use the transition group component, we need a g tag because it’s SVG-->
      <transition-group name="list" tag="g">
        <rect
          ref="rect"
          key="rect"
          class="items rect"
          width="171"
          height="171"
        />
        <circle
          id="profile"
          key="circ"
          class="items circ"
          cx="382"
          cy="203"
          r="65"
        />
        <g id="text" key="text" class="items text">
          <rect x="56" y="225" width="226" height="16" />
          <rect x="56" y="252" width="226" height="16" />
          <rect x="56" y="280" width="226" height="16" />
        </g>
        <rect
          id="footer"
          key="footer"
          class="items footer"
          y="423"
          width="155"
          height="19"
          rx="9.5"
          ry="9.5"
        />
      </transition-group>
    </svg>
    Click this ><nuxt-link to="/about">About</nuxt-link>
    <nuxt />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import AppNavigation from '~/components/AppNavigation.vue'

export default {
  components: {
    AppNavigation
  },
  computed: mapState(['page'])
}
</script>

<style lang="scss">
.items,
.list-move {
  transition: all 0.4s ease;
}

.active {
  fill: #e63946;
  .rect {
    transform: translate3d(0, 30px, 0);
  }
  .circ {
    transform: translate3d(30px, 0, 0) scale(0.5);
    color: tan;
  }
  .text {
    transform: rotate(90deg) scaleX(0.08) translate3d(-300px, -35px, 0);
    color: #e63946;
    fill: aqua;
  }
  .footer {
    transform: translateX(100px, 0, 0);
  }
}

.page-enter-active {
  transition: opacity 0.25s ease-out;
}

.page-leave-active {
  transition: opacity 0.25s ease-in;
}

.page-enter,
.page-leave-active {
  opacity: 0;
}
</style>
