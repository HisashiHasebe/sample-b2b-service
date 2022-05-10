<template>
  <div>
    <button type="button" @click="logout">
      ログアウト
      </button>
    <div>baseURL={{ $axios.defaults.baseURL }}</div>
    <div v-if="response">
      <div v-for="n in response.list" :key="n.slug">
        <nuxt-link :to="`/news/${n.topics_id}`">{{n.ymd}} {{n.subject}}</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
    middleware: 'auth',
    async asyncData ({ $axios, $config }) {
        try {
            const response = await $axios.$get('/rcms-api/1/news');
            return { response }
        }catch (e) {
            console.log(e.message)
        }
    },
     methods: {
       ...mapActions(['logout'])
     }
}
</script>