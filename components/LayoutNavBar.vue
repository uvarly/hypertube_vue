<template>
  <header v-if="this.$auth.loggedIn">
    <b-navbar
      toggleable="lg"
      variant="light"
      type="light"
      fixed="top"
      sticky
    >
      <b-navbar-brand to="/">
        <Logo class="navbar-logo" />
      </b-navbar-brand>
      <b-navbar-toggle target="nav-collapse" />
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item
            to="/"
          >
            Home
          </b-nav-item>
          <b-nav-item
            to="#"
          >
            Explore
          </b-nav-item>
          <b-nav-item
            to="#"
          >
            Profile
          </b-nav-item>
          <b-nav-item
            to="/settings"
          >
            Settings
          </b-nav-item>
          <b-nav-item
            to="#"
          >
            {{ $auth.user }}
          </b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input size="sm" class="mr-sm-2" placeholder="Browse videos" />
            <b-button size="sm" class="my-2 my-sm-0" type="submit">
              Search
            </b-button>
          </b-nav-form>
          <b-nav-item-dropdown text="Language" right>
            <b-dropdown-item href="#">
              English
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Español
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Русский
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Française
            </b-dropdown-item>
            <b-dropdown-item href="#">
              中文
            </b-dropdown-item>
            <b-dropdown-item href="#">
              日本語
            </b-dropdown-item>
          </b-nav-item-dropdown>
          <b-nav-item
            @click="logout"
            to="/"
          >
            Sign Out
          </b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </header>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  methods: {
    logout () {
      this.$auth.logout()
    }
  }
}
</script>

<style scoped>
.navbar-logo {
  width: 2vmax;
  height: 2vmax;
}

@media (max-width: 991.98px) {
  .navbar-logo {
  width: 6vmax;
  height: 6vmax;
  }
}
</style>
