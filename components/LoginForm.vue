<template>
  <b-form @submit.prevent="login">
    <b-form-group
      label="Login"
      label-for="input-username"
    >
      <b-form-input
        id="input-username"
        v-model.trim="$v.username.$model"
        type="text"
      />
      <b-form-invalid-feedback :state="!$v.username.$error">
        This field cannot be empty
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
        This field cannot be empty
      </b-form-invalid-feedback>
    </b-form-group>
    <div>
      <button
        :disabled="$v.username.$invalid || $v.password.$invalid"
        class="button--green btn-sm"
        type="submit"
      >
        Submit
      </button>
      <nuxt-link
        to="/join"
        class="button--grey btn-sm"
      >
        Join
      </nuxt-link>
    </div>
    <b-form-invalid-feedback :state="loginStatus">
      Please try again
    </b-form-invalid-feedback>
  </b-form>
</template>

<script>
import { required } from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      username: '',
      password: '',
      loginStatus: null
    }
  },
  validations: {
    username: {
      required
    },
    password: {
      required
    }
  },
  methods: {
    login () {
      this.$auth.loginWith('local', {
        data: {
          username: this.username,
          password: this.password
        }
      })
        .catch(() => {
          this.loginStatus = false
        })
    }
  }
}
</script>
