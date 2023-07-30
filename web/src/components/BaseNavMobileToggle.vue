<template>
  <button @click.prevent="handleClick" :class="{['open']: isOpen}">
    <span class="sr-only">
      {{ buttonText }} menu
    </span>
    <div class="bars">
      <span class="bar"></span>
      <span class="bar"></span>
      <span class="bar"></span>
    </div>
  </button>
</template>

<script>
import { store } from '@/store.js';

export default {
  name: 'MobileToggle',
  props: {
    menuRef: Object
  },
  computed: {
    buttonText() {
      return this.isOpen ? 'close' : 'open'
    },
    isOpen() {
      return store.isMobileNavOpen
    }
  },
  beforeUnmount () {
    document.removeEventListener('click', this.clickAway)
  },  
  methods: {
    clickAway(e) {
      if (!this.$el.contains(e.target) && !this.menuRef.contains(e.target)) {
        store.isMobileNavOpen = false
      }
    },
    handleClick() {
      store.isMobileNavOpen = !store.isMobileNavOpen;
      if (store.isMobileNavOpen) {
        document.addEventListener('click', this.clickAway)
      }
    }
  },
  watch: {
    $route() {
      store.isMobileNavOpen = false;
    }
  }
}
</script>

<style lang="scss" scoped>
button {
  @apply bg-white p-1 rounded border border-slate-200;
  aspect-ratio: 1;
  width: 40px;
}
.bars {
  position: relative;
  width: 85%;
  margin: 0 auto;
  transform: translateY(-1px)
}
.bar {
  @apply block absolute w-full bg-rose-quartz rounded;
  height: 3px;
  transition: all 0.35s ease;

  &:nth-child(2) {
    transform: translateY(-8px);
  }

  &:nth-child(3) {
    transform: translateY(8px);
  }

  .open & {
    &:nth-child(1) {
      opacity: 0;
    }

    &:nth-child(2) {
      transform: rotate(45deg);
    }

    &:nth-child(3) {
      transform: rotate(-45deg);
    }
  }
}
</style>