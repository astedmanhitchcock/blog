<template>
  <div class="mt-3 flex gap-2">
    <PostTag v-for="tag in tags" :key="tag.name" :tag="tag" />
  </div>
</template>

<script>
import PostTag from '@/components/PostTag.vue'

export default {
  name: 'TagArray',
  components: {
    PostTag
  },
  props: {
    tags: {
      type: Array,
      required: true
    }
  }
}
</script>