<template>
  <Wrapper :get-page-ready="getPageReady" class="live">
    <MainOuter class="live">
      <HeroSub
        :image="require('Images/2020/7.jpg')"
        :title="`news`"
        :get-page-ready="getPageReady"
      />
      <MainInner>
        <List :list-data="newsData" />
      </MainInner>
    </MainOuter>
  </Wrapper>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

import { pause } from 'Js/animation'
import Wrapper from '~/components/layout/Wrapper'
import MainInner from '~/components/MainInner'
import MainOuter from '~/components/MainOuter'
import HeroSub from '~/components/HeroSub'
import List from '~/components/List'

import newsData from '~/assets/json/news'

import HeadMixin from '~/mixins/Head'

export default {
  components: {
    Wrapper,
    HeroSub,
    List,
    MainInner,
    MainOuter,
  },
  mixins: [HeadMixin],
  data() {
    return {
      newsData,
      title: 'news|soratobiwo',
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
