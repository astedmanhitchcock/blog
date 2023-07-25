<template>
  <div class="flex flex-col h-full">
    <header>
      <BaseNav />
    </header>
    <div class="container p-4">
      <router-view />
    </div>
    <footer class="mt-auto">
      <div class="container p-4">
        <h4 class="font-light">© <span class="font-serif font-normal">aaronhitchcock 2023</span></h4>
      </div>
    </footer>
  </div>
</template>

<script>
import BaseNav from '@/components/BaseNav.vue'

export default {
  name: 'App',
  components: {
    BaseNav
  }
}
</script>
