<template>
  <div class="resume">
    <div class="mb-7">
      <h3 class="text-lg md:text-xl font-semibold">
        Contact:
      </h3>
      <p class="mb-1">
        <a v-if="emailString" :href="`mailto:${emailString}`" target="_blank">
          {{ emailString }}
        </a>
        <span v-if="emailString"> | </span>
        917.992.0651
      </p>
      <p class="mt-1 font-serif italic">Full stack developer with 10+ years of experience building responsive, accessible web apps and experiences for well known brands and organizations. </p>
    </div>
    <div class="mb-7">
      <h3 class="text-lg md:text-xl font-semibold">
        Proficiencies:
      </h3>
      <p>
        Javascript, Typescript, React, React Native, Vue, Ionic, Node.js, WebGL, SCSS, CSS, HTML. Experienced with Python working in Flask and Django.
      </p>
    </div>
    <div>
      <h3 class="text-lg md:text-xl font-semibold">
        Experience:
      </h3>
      <div
        v-for="(company, index) in jobs"
        :key="`${company.company}-${index}`"
        class="pb-5 pt-3"
        :class="{['mt-3 pt-5 border-t']: index > 0}"
      >
        <h3 class="font-light font-serif text-lg md:text-xl md:text-2xl mb-2">
          {{ company.company }}
        </h3>
        <div
          v-for="role in company.roles"
          :key="`${company.company}-${role.title}`"
          class="pl-5 md:pl-7"
        >
          <h4 class="text-lg font-semibold">{{ role.title }}</h4>
          <div class="font-mono md:text-base">
            <span>
              {{ role.dateStart }}
            </span>
            -
            <span v-if="role.dateDepart">
              {{ role.dateDepart }}

              <!-- 
                temporary hack to put in custom msg.
                @todo: make this customizable? Is this worth the effort?
              -->
              <span
                v-if="company.company === 'Clearing'"
                class="text-red-700"
              >
                *  Business closed due to the SVB banking crisis.
              </span>
            </span>
            <span v-else>
              current role
            </span>
          </div>
          <div 
            v-html="role.notes"
            class="mt-3"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'
import dayjs from 'dayjs'

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
            notes
          }
        }
      `,
      update: data => {
        const { allJobs } = data;
        const companies = [];
        const consolidated_jobs = allJobs.reduce((acc, curr) => {
          const {
            company,
            title,
            dateStart,
            dateDepart,
            notes
          } = curr;
          const formattedDateStart = dateStart ? dayjs(dateStart).format('MMM YYYY') : undefined
          const formattedDateDepart = dateDepart ? dayjs(dateDepart).format('MMM YYYY') : undefined;

          if (!companies.includes(company)) {
            const record = {
              company: company,
              roles: [
                {
                  title,
                  dateStart: formattedDateStart,
                  dateDepart: formattedDateDepart,
                  notes
                }
              ]
            }
            acc.push(record)
            companies.push(company)
          } else {
            const job = acc.find(el => el.company === company)
            job.roles.push({
              title,
              dateStart: formattedDateStart,
              dateDepart: formattedDateDepart,
              notes
            })
          }

          return acc;
        }, [])

        return consolidated_jobs
      }
    }
  },
  data () {
    return {
      jobs: '',
      encodedEmail: 'YXN0ZWRtYW5oaXRjaGNvY2tAZ21haWwuY29t',
      emailString: undefined
    }
  },
  mounted() {
    this.emailString = atob(this.encodedEmail)
  }
}
</script>

<style lang="scss">
.resume {

  ol, ul {
    list-style: disc;
    padding-left: 40px;

    li {
      @apply font-serif font-light text-base tracking-wide leading-7 mt-3;
    }
  }
}

</style>