<template>
  <b-container>
    <div v-if="resetStatus === null">
      <b-form @submit.prevent="resetPassword">
        <b-form-group
          label="New Password"
          label-for="input-new-password"
        >
          <b-form-input
            id="input-new-password"
            v-model.trim="$v.password.$model"
            type="password"
          />
          <b-form-invalid-feedback :state="!$v.password.$error">
            <p v-if="!$v.password.required">
              This field cannot be empty
            </p>
            <p v-else-if="!$v.password.strongPassword">
              Password must contain at least one uppercase symbol
            </p>
            <p v-else-if="!$v.password.minLength || !$v.password.maxLength">
              Password must be between 8 and 32 characters
            </p>
          </b-form-invalid-feedback>
        </b-form-group>
        <div class="links">
          <button
            :disabled="$v.password.$invalid"
            class="button--green btn-sm"
            type="submit"
          >
            Submit
          </button>
        </div>
      </b-form>
    </div>
    <div v-if="resetStatus === 204">
      <h1>Your password has been successfully reset</h1>
      <div class="d-flex justify-content-center links">
        <nuxt-link
          to="/login"
          class="button--grey"
        >
          Login
        </nuxt-link>
      </div>
    </div>
    <div v-else-if="resetStatus === 400">
      <h1>It seems taht your password has already been reset. The token is invalid</h1>
      <div class="d-flex justify-content-center links">
        <nuxt-link
          to="/"
          class="button--grey"
        >
          Back To Title
        </nuxt-link>
      </div>
    </div>
  </b-container>
</template>

<script>
import axios from 'axios'
import { helpers, required, minLength, maxLength } from 'vuelidate/lib/validators'

const strongPassword = value => !helpers.req(value) || (value !== value.toLowerCase())

export default {
  middleware: 'auth',
  auth: 'guest',
  data () {
    return {
      resetStatus: null,
      password: ''
    }
  },
  validations: {
    password: {
      required,
      strongPassword,
      minLength: minLength(8),
      maxLength: maxLength(32)
    }
  },
  methods: {
    resetPassword () {
      axios.post('http://oa-c6.21-school.ru:8081/api/v0.1/users/reset_password_confirm/', {
        uid: this.$route.params.uid,
        token: this.$route.params.token,
        new_password: this.password
      })
        .then(() => {
          this.resetStatus = 204
        })
        .catch((error) => {
          this.resetStatus = error.response.status
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
