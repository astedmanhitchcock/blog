<template>
  <div class="flex flex-col h-full"  v-on:scroll="handleScroll">
    <header
      class="header"
      :class="{['scrolling']: isScrolling}"
    >
      <BaseNav />
    </header>
    <div class="container p-4">
      <router-view />
    </div>
    <BaseFooter />
  </div>
</template>

<script>
import debounce from 'lodash/debounce';
import BaseNav from '@/components/BaseNav.vue'
import BaseFooter from './components/BaseFooter.vue';

export default {
  name: 'App',
  components: {
    BaseNav,
    BaseFooter
  },
  data() {
    return {
      scrollTop: null
    }
  },
  mounted() {
    console.log('🚀 :: welcome to aaronhitchcock.com :: 🚀')
    this.handleDebouncedScroll = debounce(this.updateScrollTop, 10);
    window.addEventListener('scroll', this.handleDebouncedScroll)
  },
  unmounted() {
      window.removeEventListener('scroll', this.handleDebouncedScroll)
  },
  computed: {
    isScrolling() {
      return this.scrollTop > 10 
    }
  },
  methods: {
    updateScrollTop() {
      this.scrollTop = window.top.scrollY
    }
  }
}
</script>

<style lang="scss" scoped>
.header {
  @apply sticky top-0 bg-base-bg drop-shadow-none transition;

  &.scrolling {
    @apply drop-shadow-lg;
  }
}
</style>
