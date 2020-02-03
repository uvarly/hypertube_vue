<template>
  <b-container>
    <b-form @submit.prevent="reset" v-if="resetStatus === null">
      <b-form-group
        label="Tell us your Email"
        label-for="input-email"
      >
        <b-form-input
          id="input-email"
          v-model.trim="$v.email.$model"
          type="email"
        />
        <b-form-invalid-feedback :state="!$v.email.$error">
          <p v-if="!$v.email.required">
            This field cannot be empty
          </p>
          <p v-else-if="!$v.email.email">
            Not a valid email
          </p>
        </b-form-invalid-feedback>
      </b-form-group>
      <div class="links">
        <button
          :disabled="$v.email.$invalid"
          class="button--green btn-sm"
          type="submit"
        >
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
    <h1 v-else-if="resetStatus === true">
      Link has been sent
    </h1>
    <h1 v-else-if="resetStatus === false">
      Something went wrong. Try again
    </h1>
  </b-container>
</template>

<script>
import axios from 'axios'
import { required, email } from 'vuelidate/lib/validators'

export default {
  middleware: 'auth',
  auth: 'guest',
  data () {
    return {
      resetStatus: null,
      email: ''
    }
  },
  validations: {
    email: {
      required,
      email
    }
  },
  methods: {
    reset () {
      axios.post('http://oa-c6.21-school.ru:8081/api/v0.1/users/reset_password/', {
        email: this.email
      })
        .then(() => {
          this.resetStatus = true
        })
        .catch(() => {
          this.resetStatus = false
        })
    }
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
.links {
  padding-top: 15px;
}
</style>
