<template>
  <div
    :class="[{ 'is-open': $store.state.route.fullPath === '/' || getMenuOpen }]"
    class="menu"
  >
    <div class="menu__inner">
      <ul class="menu__list">
        <li v-if="!getIsDesktop" class="menu__item">
          <span class="menu__item-inner">
            <nuxt-link
              :to="`/`"
              @click="setMenuOpen(false)"
              class="menu__target"
              >home</nuxt-link
            >
          </span>
        </li>
        <li
          v-for="(item, index) in links"
          :key="`menu${index}`"
          class="menu__item"
        >
          <span class="menu__item-inner">
            <nuxt-link
              :to="`/${item}/`"
              @click="setMenuOpen(false)"
              v-html="item"
              class="menu__target"
            />
          </span>
        </li>
      </ul>
    </div>
    <div class="menu__bg" />
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  props: {
    getMenuOpen: {
      type: Boolean,
      default: false,
    },
    getIsDesktop: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      /**
       * ID List
       */
      links: ['news', 'live', 'profile', 'listen', 'follow'],
    }
  },
  computed: {
    //
  },
  methods: {
    ...mapActions(['setMenuOpen']),
  },
}
</script>

<style lang="scss" scoped>
.menu {
  position: fixed;
  top: calc(100vh * 200 / 667);
  left: calc(100vw * 10 / 375);
  z-index: $z-menu;
  overflow: hidden;
  pointer-events: none;
  opacity: 0;
  //
  @include desktop {
    top: auto;
    bottom: calc(100vh * 114 / 768);
    left: calc(100vw * 45 / 1024);
  }
  //
  @include widescreen {
    bottom: calc(100vh * 90 / 800);
    left: calc(100vw * 80 / 1280);
  }
  //
  &.is-open {
    pointer-events: auto;
    opacity: 1;
  }
}

.menu__bg {
  z-index: 1;
  background-color: $color-gray-level1;
  //
  @include overlay;
}

.menu__inner {
  position: relative;
  z-index: 9;
  //
  @include desktop {
    //
  }
}

.menu__list {
  //
}

.menu__item {
  margin-top: calc(100vw * 4 / 375 * -1);
  margin-bottom: calc(100vw * 6 / 375 * -1);
  overflow: hidden;
  text-align: right;
  //
  @include desktop {
    margin-top: calc(100vh * 8 / 768 * -1);
    margin-bottom: calc(100vh * 12 / 768 * -1);
  }
  //
  + .menu__item {
    margin-top: calc(100vw * 5 / 375);
    //
    @include desktop {
      margin-top: calc(100vw * 2 / 375);
    }
  }
}

.menu__item-inner {
  display: inline-block;
  //will-change: transform;
  //transition: transform 0.6s $easeInOutLongExpo;
  //transform: translateY(125%);
  //
  @include desktop {
    //
  }
  //
  .menu.is-open & {
    //transform: translateY(0);
  }
}

.menu__target {
  position: relative;
  display: inline-block;
  font-family: $font-Nunito;
  font-size: calc(100vw * 40 / 375);
  font-weight: $font-Nunito-bold;
  color: $color-white;
  text-transform: uppercase;
  //
  @include desktop {
    font-size: calc(100vh * 80 / 768);
    //
    &::after {
      z-index: -1;
      content: '';
      background-color: $color-red;
      transition: transform 1s $easePowerInOut;
      transform: scaleX(0);
      transform-origin: left center;
      //
      @include overlay;
    }
    //
    &:hover {
      &::after {
        transform: scaleX(1);
        transform-origin: right center;
      }
    }
  }
  //
  @include widescreen {
    font-size: calc(100vh * 80 / 800);
  }
}
</style>
