<template>
  <footer class="mt-auto">
    <div class="container p-4">
      <h4 class="font-light">
        © <LogoLink />
        <span class="font-serif font-normal">2023</span>
      </h4>
    </div>
  </footer>
</template>

<script>
import LogoLink from './LogoLink.vue';

export default {
  name: 'BaseFooter',
  components: {
    LogoLink
  }
}
</script>