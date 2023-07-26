<template>
  <h2 class="base-page-title">resume</h2>
  <div
    v-for="(job, index) in jobs"
    :key="`${job.company}-${job.title}`"
    class="py-3"
    :class="{['mt-3 border-t']: index > 0}"
  >
    <h3 class="font-light font-serif text-lg">{{ job.company }}</h3>
    <h4 class="text-lg font-semibold">{{ job.title }}</h4>
    <div class="font-mono">
      <span>
        {{ job.dateStart }}
      </span>
      -
      <span v-if="job.dateDepart">
        {{ job.dateDepart }}
      </span>
      <span v-else>
        current role
      </span>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'ResumePage',
  apollo: {
    jobs: {
      query: gql`
        query {
          allJobs {
            company
            title
            dateStart
            dateDepart
          }
        }
      `,
      update: data => data.allJobs
    }
  },
  data () {
    return {
      jobs: ''
    }
  },
  watch: {
    jobs() {
      console.log('JOBS :: ', this.jobs)
    }
  }
}
</script>