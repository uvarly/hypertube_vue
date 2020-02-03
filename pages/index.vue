<template>
  <div>
    <b-container v-if="!this.$auth.loggedIn">
      <div>
        <LogoDesktop class="logo" />
        <h1 class="title">
          HYPERTUBE
        </h1>
        <h2 class="subtitle">
          Better than YouTube
        </h2>
        <div class="d-flex justify-content-center links">
          <nuxt-link
            to="/login"
            class="button--green"
          >
            Log in
          </nuxt-link>
          <nuxt-link
            to="/join"
            class="button--grey"
          >
            Join
          </nuxt-link>
        </div>
      </div>
    </b-container>
  </div>
</template>

<script>
import LogoDesktop from '~/components/LogoDesktop.vue'

export default {
  components: {
    LogoDesktop
  },
  data () {
    return {}
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

.logo {
  animation: 1s appear;
  width: 24vmax;
  height: 12vmax;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 100;
  font-size: 5vmax;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 2.5vmax;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

@keyframes appear {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@media (max-width: 991.98px) {
  .title {
    font-size: 8vmax;
  }

  .subtitle {
    font-size: 4vmax;
  }

  .logo {
    width: 36vmax;
    height: 18vmax;
  }
}
</style>
