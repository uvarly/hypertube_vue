<template>
  <b-container>
    <div>
      <nuxt-link to="/">
        <Logo class="logo" />
      </nuxt-link>
      <LoginForm />
    </div>
  </b-container>
</template>

<script>
import Logo from '~/components/Logo.vue'
import LoginForm from '~/components/LoginForm.vue'

export default {
  middleware: 'auth',
  auth: 'guest',
  components: {
    Logo,
    LoginForm
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 50vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.logo {
  animation: 1s appear;
  width: 3vmax;
  height: 3vmax;
}

@keyframes appear {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 100;
  }
}

@media (max-width: 991.98px) {
  .logo {
    width: 10vmax;
    height: 10vmax;
  }
}
</style>
