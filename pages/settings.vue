<template>
  <b-card no-body>
    <b-tabs v-model="tabIndex" small card align="center">
      <b-tab title="General">
        <b-card-body class="text-center">
          <b-card-text>
            Nothing here yet
          </b-card-text>
        </b-card-body>
      </b-tab>
      <b-tab title="Change Username">
        <b-card-text>
          <SettingsUsernameForm />
        </b-card-text>
      </b-tab>
      <b-tab title="Change Password">
        <b-card-text>
          <!-- <SettingsPasswordForm /> -->
        </b-card-text>
      </b-tab>
    </b-tabs>
  </b-card>
</template>

<script>
import SettingsUsernameForm from '~/components/SettingsUsernameForm.vue'
// import SettingsPasswordForm from '~/components/SettingsPasswordForm.vue'

export default {
  middleware: 'auth',
  components: {
    SettingsUsernameForm
    // SettingsPasswordForm
  },
  data () {
    return {
      tabIndex: 0,
      currentForm: null
    }
  }
}
</script>

<style scoped>

</style>
