<template>
  <div>
    <h1>{{ response.details.ext_col_01}}</h1>
    <p>{{ response.details.ext_col_02}}</p>

  <button type="button" @click="logout">
  ログアウト
  </button>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  middleware: 'auth',
  async asyncData({$axios}) {
    try {
      const response = await $axios.$get(process.env.BASE_URL + '/rcms-api/4/service_top/4')
      return { response }
    } catch (e) {
      console.log(e.message)
    }
  },
  methods: {
    ...mapActions(['logout'])
  }
}
</script>