<template>
  <nav class="base-nav">
    <div class="relative bg-base-bg w-full md:w-auto z-10">
      <div class="base-nav__header">
        <h1>
          <LogoLink />
        </h1>
        <MobileToggle class="md:hidden" :menu-ref="$refs.menu" />
      </div>
    </div>
    <div ref="menu" class="base-nav__menu" :class="{['base-nav__menu--open']: isMobileNavOpen }">
      <router-link
        v-for="(link, index) in links"
        :key="link.path"
        :to="link.path"
        class="relative text-rose-quartz / py-3 md:px-2 md:py-1"
        :class="{
          'border-t md:border-l md:border-t-0': index > 0
        }"
      >
        {{ link.label }}
      </router-link>
    </div>
  </nav>
</template>

<script>
import { store } from '@/store.js';
import LogoLink from '@/components/LogoLink.vue';
import MobileToggle from '@/components/BaseNavMobileToggle.vue'

export default {
  name: 'BaseNav',
  components: {
    LogoLink,
    MobileToggle
  },
  data() {
    return {
      links: [
      {
          'label': 'cv',
          'path': '/cv'
        },
        {
          'label': 'styleguide',
          'path': '/styleguide'
        }
      ]
    }
  },
  computed: {
    isMobileNavOpen() {
      return store.isMobileNavOpen
    }
  },
  methods: {
    handleLinkClick() {
      store.isMobileNavOpen = false
    }
  }
}
</script>

<style lang="scss" scoped>
.base-nav {
  @apply relative w-full flex items-center justify-between bg-base-bg mx-auto max-w-screen-md lg:max-w-screen-lg;

  &__header {
    @apply mx-auto p-4 flex justify-between items-center w-full max-w-screen-sm md:max-w-screen-md;
  }

  &__menu {
    @apply absolute w-full left-0 top-full flex flex-col bg-white px-4
      md:relative md:w-auto md:left-auto md:top-auto md:flex-row md:bg-transparent md:px-4 md:drop-shadow-none;
    width: 100vw;
    left: 50%;
    transform: translate(-50%, -100%);
    transition: transform 0.35s ease;

    &--open {
      @apply drop-shadow-lg;
      transform: translate(-50%, 0);
    }

    @media (min-width: 768px) {
      transform: translate(0);
      opacity: 1;
      z-index: 0;
      width: auto;
      left: auto;
      filter: drop-shadow(0 0 #0000);

      &:after,
      &:before {
        display: none;
      }
    }
  }
}
</style>