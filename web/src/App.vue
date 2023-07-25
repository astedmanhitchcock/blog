<template>
  <div class="flex flex-col h-full min-h-screen">
    <header class="sticky top-0 bg-base-bg">
      <BaseNav />
    </header>
    <div class="container p-4">
      <router-view />
    </div>
    <BaseFooter />
  </div>
</template>

<script>
import BaseNav from '@/components/BaseNav.vue'
import BaseFooter from './components/BaseFooter.vue';

export default {
  name: 'App',
  components: {
    BaseNav,
    BaseFooter
  }
}
</script>
