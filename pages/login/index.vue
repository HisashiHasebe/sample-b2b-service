<template>
    <form @submit.prevent="login">
      <p v-if="loginStatus !== null" :style="{ color: resultMessageColor }">
        {{ resultMessage }}
      </p>

        <input v-model="sitekey" name="sitekey" type="sitekey" placeholder="sitekey">
        <input v-model="email" name="email" type="email" placeholder="email">
        <input
            v-model="password"
            name="password"
            type="password"
            placeholder="password"
        >
        <button type="submit">
            ログイン
        </button>

        <div>
            <nuxt-link to="/news/">
                ニュース一覧ページへ
            </nuxt-link>
        </div>
        <div>
            <nuxt-link to="/owners-page/">
                契約者専用ページへ
            </nuxt-link>
        </div>
    </form>
</template>

<script>
export default {
    data () {
        return {
            sitekey: '',
            email: '',
            password: '',
            loginStatus: null,
            resultMessage: null
        }
    },
    computed: {
        resultMessageColor () {
            switch (this.loginStatus) {
            case 'success':
                return 'green'
            case 'failure':
                return 'red'
            default:
                return ''
            }
        }
    },
    methods: {
        async login () {
            localStorage.setItem('sitekey', this.sitekey);
            this.$axios.defaults.baseURL = `https://${this.sitekey}.g.kuroco.app`;
            try {
                const payload = {
                    email: this.email,
                    password: this.password
                }
                await this.$store.dispatch('login', payload)
                this.loginStatus = 'success'
                this.resultMessage = 'ログインに成功しました。'
            } catch (e) {
                this.loginStatus = 'failure'
                this.resultMessage = 'ログインに失敗しました。'
            }
        }
    }
}
</script>