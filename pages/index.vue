<template>
  <section class="section container content">
    <h1>
      Nuxt.js Advent Calendar 2019
    </h1>

    <p>{{ comment }}</p>

    <table class="table is-bordered">
      <thead>
        <tr>
          <th
            v-for="dayName in dayNames"
            :key="dayName"
            class="week"
          >
            {{ dayName }}
          </th>
        </tr>
      </thead>

      <tbody>
        <tr
          v-for="index in [0, 1, 2]"
          :key="index"
        >
          <th
            v-for="day in days.slice((7 * index), (7 + (7 * index)))"
            :key="day.date"
            class="week"
          >
            <p class="tag is-primary is-light is-medium">
              {{ day.date }}
            </p>

            <article class="media">
              <div class="media-content">
                <img
                  class="image is-48x48"
                  :src="day.authorImageUrl"
                >

                <a
                  :href="`https://qiita.com/${day.authorName}`"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="has-text-weight-normal is-size-6 has-text-info"
                >
                  {{ day.authorName }}
                </a>

                <div class="media content">
                  <a v-if="day.articleUrl !== null"
                    :href="day.articleUrl"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="has-text-info is-6"
                  >
                    {{ day.comment }}
                  </a>

                  <p v-else
                    class="has-text-dark is-6"
                  >
                    {{ day.comment }}
                  </p>
                </div>
              </div>
            </article>
          </th>
        </tr>

        <tr>
          <th
            v-for="day in days.slice(21)"
            :key="day.date"
            class="week"
          >
            <p class="tag is-primary is-light is-medium">
              {{ day.date }}
            </p>

            <article class="media">
              <div class="media-content">
                <img
                  class="image is-48x48"
                  :src="day.authorImageUrl"
                >

                <a
                  :href="`https://qiita.com/${day.authorName}`"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="has-text-weight-normal is-size-6 has-text-info"
                >
                  {{ day.authorName }}
                </a>

                <div class="media content">
                  <a v-if="day.articleUrl !== null"
                    :href="day.articleUrl"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="has-text-info is-6"
                  >
                    {{ day.comment }}
                  </a>

                  <p v-else
                    class="has-text-dark is-6"
                  >
                    {{ day.comment }}
                  </p>
                </div>
              </div>
            </article>
          </th>

          <th
            v-for="date in [26, 27, 28]"
            :key="date"
          >
            <p class="tag is-light is-medium">
              {{ date }}
            </p>
          </th>
        </tr>
      </tbody>
    </table>

    <p>※ このページはレスポンシブ対応していません。デスクトップサイズの画面でご覧ください。</p>
  </section>
</template>

<script>
import { parse } from 'node-html-parser'

export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get('https://qiita.com/advent-calendar/2019/nuxt-js')
    const root = parse(data)
    return {
      comment: root.querySelector('.markdownContent').text,
      dayNames: root.querySelectorAll('.adventCalendarCalendar_dayName').map(dayName => dayName.text),
      days: root.querySelectorAll('.adventCalendarCalendar_day').map(day => {
        const articleUrl = day.querySelector('.adventCalendarCalendar_comment').querySelector('a') ?
          day.querySelector('.adventCalendarCalendar_comment').querySelector('a').attributes['href'] :
          null
        return {
          date: day.querySelector('.adventCalendarCalendar_date').text,
          authorName: day.querySelector('.adventCalendarCalendar_author').text.replace(/\s|&nbsp;/g, ''),
          authorImageUrl: day.querySelector('.adventCalendarCalendar_authorIcon').attributes['src'],
          comment: day.querySelector('.adventCalendarCalendar_comment').text,
          articleUrl: articleUrl
        }
      })
    }
  }
}
</script>

<style>
.week {
  width: calc(100% / 7);
}
</style>
