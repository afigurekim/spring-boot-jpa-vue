<template>
    <div class="login-view">
        <h1>Login Page</h1>
        <LoginForm :onlogin="handleLogin" />
    </div>
</template>

<script>
import LoginForm from '@/components/molecules/LoginForm.vue'
export default {
    name: 'LoginView',
    components: { LoginForm },
    methods: { handleLogin (authInfo) {
        return this.$store.dispatch('login', authInfo)
            .then(() => {
                this.$router.push({ path: '/' })
            })
            .catch(err => this.throwReject(err))
    },
    throwReject (err) { return Promise.reject(err) }
    }
}
</script>

<style scoped>
.login-view {
    width: 320px;
    margin: auto;
}
</style>
