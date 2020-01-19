<template>
  <b-container>
    <div>
      <nuxt-link to="/">
        <Logo class="logo" />
      </nuxt-link>
      <JoinForm />
    </div>
  </b-container>
</template>

<script>
import Logo from '~/components/Logo.vue'
import JoinForm from '~/components/JoinForm.vue'

export default {
  components: {
    Logo,
    JoinForm
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 66vh;
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
