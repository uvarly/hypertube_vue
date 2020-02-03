<template>
  <b-form>
    <b-form-group
      label="Login"
      label-for="input-username"
    >
      <b-form-input
        id="input-username"
        type="text"
      />
      <b-form-invalid-feedback :state="!$v.username.$error">
        This field cannot be empty
      </b-form-invalid-feedback>
    </b-form-group>
  </b-form>
</template>

<script>
export default {

}
</script>

<style scoped>

</style>
