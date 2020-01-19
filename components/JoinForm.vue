<template>
  <b-form @submit.prevent="register">
    <b-form-group
      label="Username"
      label-for="input-username"
    >
      <b-form-input
        id="input-username"
        v-model.trim="$v.username.$model"
        type="text"
      />
      <b-form-invalid-feedback :state="!$v.username.$error">
        <p v-if="!$v.username.required">
          This field cannot be empty
        </p>
        <p v-else-if="!$v.username.alphaNum">
          Only alphanumerical symbols allowed
        </p>
      </b-form-invalid-feedback>
    </b-form-group>
    <b-form-group
      label="Email"
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
    <b-form-group
      label="Password"
      label-for="input-password"
    >
      <b-form-input
        id="input-password"
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
    <div>
      <button
        :disabled="$v.username.$invalid || $v.email.$invalid || $v.password.$invalid"
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
    <b-form-invalid-feedback :state="registerStatus">
      Try any other username or email
    </b-form-invalid-feedback>
  </b-form>
</template>

<script>
import axios from 'axios'
import { helpers, required, alphaNum, email, minLength, maxLength } from 'vuelidate/lib/validators'

const strongPassword = value => !helpers.req(value) || (value !== value.toLowerCase())

export default {
  data () {
    return {
      username: 'admin',
      email: 'biba@fuck.you',
      password: '130547',
      registerStatus: null
    }
  },
  validations: {
    username: {
      required,
      alphaNum
    },
    email: {
      required,
      email
    },
    password: {
      required,
      strongPassword,
      minLength: minLength(8),
      maxLength: maxLength(32)
    }
  },
  methods: {
    register () {
      axios
        .post('http://vo-c1.21-school.ru:8081/api/v0.1/users/', {
          username: this.username,
          email: this.email,
          password: this.password
        })
        .catch(() => {
          this.registerStatus = false
        })
    }
  }
}
</script>
