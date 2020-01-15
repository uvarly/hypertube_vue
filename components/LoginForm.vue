<template>
  <b-form @submit.prevent="login">
    <b-form-group
      label="Login"
      label-for="input-username"
    >
      <b-form-input
        id="input-username"
        v-model="form.username"
        type="text"
        required
        placeholder="Username"
      />
    </b-form-group>
    <b-form-group
      label="Password"
      label-for="input-password"
    >
      <b-form-input
        id="input-password"
        v-model="form.password"
        type="password"
        required
        placeholder="Password"
      />
    </b-form-group>
    <nuxt-link
      to="/recover"
    >
      Forgot password?
    </nuxt-link>
    <div>
      <button class="button--green btn-sm" type="submit">
        Submit
      </button>
      <nuxt-link
        to="/join"
        class="button--grey btn-sm"
      >
        Join
      </nuxt-link>
    </div>
    <b-form-invalid-feedback :state="validateForm">
      Please try again
    </b-form-invalid-feedback>
  </b-form>
</template>

<script>
export default {
  data () {
    return {
      form: {
        username: '',
        password: ''
      },
      errors: []
    }
  },
  computed: {
    validateForm () {
      return this.errors.length === 0
    }
  },
  methods: {
    login () {
      this.$auth.loginWith('local', {
        data: this.form
      })
        .catch((error) => {
          this.errors.push(error)
        })
    }
  }
}
</script>
