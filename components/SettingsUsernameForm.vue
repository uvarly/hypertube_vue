<template>
  <b-container>
    <b-form @submit.prevent="changeUsername" v-if="usernameChangeStatus === null">
      <b-form-group
        label="New Username"
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
        </b-form-invalid-feedback>
      </b-form-group>
      <div class="links">
        <button
          :disabled="$v.username.$invalid || $v.password.$invalid"
          class="button--green btn-sm"
          type="submit"
        >
          Submit
        </button>
      </div>
    </b-form>
  </b-container>
</template>

<script>
import axios from 'axios'
import { required, alphaNum } from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      usernameChangeStatus: null,
      username: '',
      password: ''
    }
  },
  validations: {
    username: {
      required,
      alphaNum
    },
    password: {
      required
    }
  },
  methods: {
    changeUsername () {
      axios.defaults.withCredentials = true
      axios
        .post('http://oa-c6.21-school.ru:8081/api/v0.1/users/set_username/', {
          new_username: this.username,
          current_password: this.password
        })
        .then(() => {
          this.usernameChangeStatus = true
        })
        .catch(() => {
          this.usernameChangeStatus = false
        })
    }
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.links {
  padding-top: 15px;
}
</style>
