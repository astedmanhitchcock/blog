<template>
  <div class="post" v-if="post">
    <div class="mb-6">
      <h2 class="font-medium">
        {{ post.title }}{{ post.subtitle &&  `:  ${post.subtitle}` }}
      </h2>
      <span class="block">
        by <AuthorLink :author="post.author" />
      </span>
      <span class="font-mono">
        {{ displayableDate(post.publishDate) }}
      </span>
      <p v-if="post.metaDescription">
        {{ post.metaDescription }}
      </p>
    </div>
    <article v-html="post.body">
    </article>
    <span class="clear-both block"></span>
    <TagArray :tags="post.tags" />
  </div>
</template>

<script>
import gql from 'graphql-tag'
import AuthorLink from '@/components/AuthorLink'
import TagArray from '@/components/TagArray.vue'

export default {
  name: 'PostDetail',
  components: {
    AuthorLink,
    TagArray
  },
  data () {
    return {
      post: null,
    }
  },
  apollo: {
    post: {
      query: gql`query ($slug: String!) {
        postBySlug(slug: $slug) {
          title
          subtitle
          publishDate
          metaDescription
          slug
          body
          author {
            user {
              username
              firstName
              lastName
            }
          }
          tags {
            name
          }
        }
      }`,
      variables() {
        return {
          slug: this.$route.params.slug
        }
      },
      update: (data) => {
        return data.postBySlug
      }
    }
  },
  methods: {
    displayableDate (date) {
      return new Intl.DateTimeFormat(
        'en-US',
        { dateStyle: 'full' },
      ).format(new Date(date))
    }
  },
  watch: {
    post() {
      console.log('loaded the post :: ', this.post)
    }
  }
}
</script>