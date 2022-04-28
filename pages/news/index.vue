<template>
  <div>
    <button type="button" @click="logout">
      ログアウト
      </button>
    <div>baseURL={{ $config.baseURL}}</div>
    <div v-for="n in response.list" :key="n.slug">
      <nuxt-link :to="'/news/'+ n.slug">{{n.ymd}} {{n.subject}}</nuxt-link>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
    middleware: 'auth',
    async asyncData ({ $axios, $config }) {
        try {
            const response = await $axios.$get($config.baseURL + '/rcms-api/1/news')
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