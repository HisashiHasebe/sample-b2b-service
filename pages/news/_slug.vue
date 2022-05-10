<template>
    <div v-if="response">
      <h1 class="title">{{ response.details.subject }}</h1>
      <div class="post" v-html="response.details.contents"></div>
    </div>
</template>

<script>
export default {
    middleware: 'auth',
    async asyncData ({ $axios, params, $config }) {
        try {
            const response = await $axios.$get(`/rcms-api/1/newsdetail/${params.slug}`)
            return { response }
        }catch (e) {
            console.log(e.message)
        }
    }
}
</script>