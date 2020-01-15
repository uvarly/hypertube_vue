<template>
  <b-form @submit.prevent="register">
    <b-form-group
      label="Username"
      label-for="input-login"
    >
      <b-form-input
        id="input-login"
        :state="validateLogin"
        v-model="form.login"
        type="text"
        required
        placeholder="Login"
      />
    </b-form-group>
    <b-form-invalid-feedback :state="validateLogin">
      Please try again
    </b-form-invalid-feedback>
    <b-form-group
      label="Email"
      label-for="input-email"
    >
      <b-form-input
        id="input-email"
        v-model="form.email"
        type="email"
        required
        placeholder="Email"
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
    <b-form-group
      label="Confirm password"
      label-for="input-password-confirm"
    >
      <b-form-input
        id="input-password-confirm"
        v-model="form.password_confirm"
        type="password"
        required
        placeholder="Password confirmation"
      />
    </b-form-group>
    <div>
      <button class="button--green btn-sm" type="submit">
        Submit
      </button>
      <nuxt-link
        to="/"
        class="button--grey btn-sm"
      >
        Back To Title
      </nuxt-link>
    </div>
  </b-form>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      form: {
        login: 'admin',
        email: 'somerussianlad@gmail.com',
        password: '123123123',
        password_confirm: '123123123'
      }
    }
  },
  methods: {
    register () {
      axios.post('http://vo-c1.21-school.ru:8081/api/v0.1/users/', {
        username: this.form.login,
        email: this.form.email,
        password: this.form.password,
        password_confirm: this.form.password_confirm
      })
    },
    validateLogin () {
      return this.form.login
    }
  }
}
</script>
