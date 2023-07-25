<template>
  <nav class="base-nav container p-4 flex items-center justify-between">
    <h1>
      <LogoLink />
    </h1>
    <div>
      <div class="base-nav__menu" :class="{['base-nav__menu--open']: isMobileMenuOpen}">
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
      <MobileToggle class="md:hidden" @change="handleToggleChange" />
    </div>
  </nav>
</template>

<script>
import LogoLink from './LogoLink.vue';
import MobileToggle from '@/components/BaseNavMobileToggle.vue'

export default {
  name: 'BaseNav',
  components: {
    LogoLink,
    MobileToggle
  },
  data() {
    return {
      isMobileMenuOpen: false,
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
  methods: {
    handleClickAway() {

    },
    handleToggleChange(isOpen) {
      this.isMobileMenuOpen = isOpen
    }
  }
}
</script>

<style lang="scss" scoped>
.base-nav {
  @apply bg-base-bg;
  position: relative;
  z-index: 1;

  &__menu {
    @apply absolute w-full left-0 top-full flex flex-col bg-white px-4 
      md:relative md:w-auto md:left-auto md:top-auto md:flex-row md:bg-transparent md:px-4;
    transform: translateY(-100%);
    opacity: 0;
    z-index: -1;
    transition: transform 0.35s ease, opacity 0.35s ease;

    &:before {
      @apply absolute top-0;
      content: '';
      display: block;
      height: 100%;
      width: 200vw;
    }

    &:before {
      @apply bg-white drop-shadow-xl;
      left: -50vw;
    }
    
    &--open {
      transform: translateY(0);
      opacity: 1;
    }

    @media (min-width: 768px) {
      transform: translateY(0);
      opacity: 1;
      z-index: 0;

      &:after,
      &:before {
        display: none;
      }
    }
  }
}
</style>