<template>
  <Wrapper :get-page-ready="getPageReady" class="profile">
    <MainOuter>
      <HeroSub
        :image="require('Images/2020/8.jpg')"
        :title="`profile`"
        :get-page-ready="getPageReady"
      />
      <MainInner>
        <div
          v-for="(item, index) in profileData"
          :key="`profileSection${index}`"
          class="profile__section"
        >
          <Title2 :item="item" />
          <div v-if="item.artistImage" class="profile__artist-wrap">
            <img
              :src="require(`Images/${item.artistImage}`)"
              alt="artist image"
              class="profile__artist"
            />
          </div>
          <p v-if="item.text" v-html="item.text" class="profile__text" />
        </div>
      </MainInner>
    </MainOuter>
  </Wrapper>
</template>

<style lang="scss" scoped>
.profile__section {
  font-weight: bold;
  color: $color-white;
  text-align: justify;
  //
  @include desktop {
    padding-left: calc(100vw * 90 / 1024);
  }
  //
  + .profile__section {
    margin-top: calc(100vw * 20 / 375);
    //
    @include desktop {
      margin-top: calc(100vw * 100 / 1024);
    }
  }
}

.profile__artist-wrap {
  margin-right: calc(100vw * 30 / 375 * -1);
  margin-bottom: 20px;
  margin-left: calc(100vw * 30 / 375 * -1);
  //
  @include desktop {
    margin-right: calc(100vw * 30 / 1024 * -1);
    margin-bottom: calc(100vw * 35 / 1024);
    margin-left: calc(100vw * 30 / 1024 * -1 + 100vw * 90 / 1024 * -1);
  }
}

.profile__artist {
  //
}

.profile__text {
  position: relative;
  max-width: 550px;
  font-size: 1.2rem;
  line-height: 1.95;
  //
  @include desktop {
    font-size: 1.4rem;
    line-height: 2.25;
  }
  //
  @include fullhd {
    max-width: 650px;
    font-size: 1.6rem;
    line-height: 2.5;
  }
}
</style>

<script>
import { mapActions, mapGetters } from 'vuex'

import { pause } from 'Js/animation'
import Wrapper from '~/components/layout/Wrapper'
import MainInner from '~/components/MainInner'
import MainOuter from '~/components/MainOuter'
import HeroSub from '~/components/HeroSub'
import Title2 from '~/components/Title2'

import profileData from '~/assets/json/profile'

import HeadMixin from '~/mixins/Head'

export default {
  components: {
    Title2,
    Wrapper,
    HeroSub,
    MainOuter,
    MainInner,
  },
  mixins: [HeadMixin],
  data() {
    return {
      profileData,
      title: 'profile|soratobiwo',
    }
  },
  computed: {
    ...mapGetters([
      'getPageReady',
      'getPageHeight',
      'getPageWidth',
      'getPageScrollY',
      'getMenuOpen',
    ]),
  },
  mounted() {
    this.$nextTick(async () => {
      await pause(0.1)
      this.setPageReady(true)
    })
  },
  methods: {
    ...mapActions(['setPageReady']),
  },
}
</script>
