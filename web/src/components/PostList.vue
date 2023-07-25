<template>
  <ol>
    <li
      v-for="post, idx in publishedPosts"
      :key="post.title"
      class="py-3"
      :class="{['border-t']: idx > 0}"
    >
      <router-link
        :to="`/post/${post.slug}`"
        class="hover:underline"
      >
        <h2 class="font-medium">
          {{ post.title }}{{ post.subtitle &&  `:  ${post.subtitle}` }}
        </h2>
      </router-link>
      <span v-if="showAuthor" class="block">
        by <AuthorLink :author="post.author" />
      </span>
      <span class="font-mono">
        {{ displayableDate(post.publishDate) }}
      </span>
      <p v-if="post.metaDescription">
        {{ post.metaDescription }}
      </p>
      <TagArray :tags="post.tags" />
    </li>
  </ol>
</template>

<script>
import AuthorLink from '@/components/AuthorLink'
import TagArray from '@/components/TagArray.vue'

export default {
  name: 'PostList',
  components: {
    AuthorLink,
    TagArray
  },
  props: {
    posts: {
      type: Array,
      required: true,
    },
    showAuthor: {
      type: Boolean,
      required: false,
      default: true,
    },
  },
  computed: {
    publishedPosts () {
      return this.posts.filter(post => post.published)
    }
  },
  methods: {
    displayableDate (date) {
      if (date) {
        return new Intl.DateTimeFormat(
          'en-US',
          { dateStyle: 'full' },
        ).format(new Date(date)).toLowerCase()
      } else {
        return "no date"
      }
    }
  },
}
</script>
