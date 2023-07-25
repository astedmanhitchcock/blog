<template>
  <router-link
    :to="to"
    class="font-serif font-normal text-jet hover:text-cerulean"
  >
    aaronhitchcock
  </router-link>
</template>

<script>
export default {
  name: 'LogoLink',
  props: {
    to: {
      type: String,
      default: () => '/'
    },
  }
}
</script>