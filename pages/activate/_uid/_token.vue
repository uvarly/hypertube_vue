<template>
  <b-container>
    <div v-if="activationStatus === 204">
      <h1>Thank you for joining us</h1>
      <div class="d-flex justify-content-center links">
        <nuxt-link
          to="/login"
          class="button--grey"
        >
          Login
        </nuxt-link>
      </div>
    </div>
    <div v-else-if="activationStatus === 400">
      <h1>Hey buddy, I think you've got the wrong door</h1>
      <div class="d-flex justify-content-center links">
        <nuxt-link
          to="/"
          class="button--grey"
        >
          To The Leather Club
        </nuxt-link>
      </div>
    </div>
    <div v-else-if="activationStatus === 403">
      <h1>Link is no longer active. Sorry, mate</h1>
      <div class="d-flex justify-content-center links">
        <nuxt-link
          to="/"
          class="button--grey"
        >
          to Index Page
        </nuxt-link>
      </div>
    </div>
  </b-container>
</template>

<script>
import axios from 'axios'

export default {
  middleware: 'auth',
  auth: 'guest',
  data () {
    return {
      activationStatus: null
    }
  },
  mounted () {
    this.activateAccount()
  },
  methods: {
    activateAccount () {
      axios.post('http://vo-c1.21-school.ru:8081/api/v0.1/users/activation/', {
        uid: this.$route.params.uid,
        token: this.$route.params.token
      })
        .then(() => {
          this.activationStatus = 204
        })
        .catch((error) => {
          this.activationStatus = error.response.status
        })
    }
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.links {
  padding-top: 15px;
}
</style>
