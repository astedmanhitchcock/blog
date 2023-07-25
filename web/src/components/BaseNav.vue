<template>
  <nav class="container p-4 flex justify-between">
    <div>
      <router-link
        :to="'/'"
      >
        <h1 class="font-serif font-normal text-jet hover:text-cerulean">aaronhitchcock</h1>
      </router-link>
    </div>
    <div>
      <router-link
        v-for="(link, index) in links"
        :key="link.path"
        :to="link.path"
        class="text-rose-quartz / py-1 px-2"
        :class="{
          'border-l': index > 0
        }"
      >
        {{ link.label }}
      </router-link>
      <MobileToggle class="lg:hidden" />
    </div>
  </nav>
</template>

<script>
import MobileToggle from '@/components/BaseNavMobileToggle.vue'

export default {
  name: 'BaseNav',
  components: {
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
  }
}
</script>