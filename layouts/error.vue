<template>
  <div class="container">
    <h1>
      You picked the wrong house, fool
    </h1>
    <nuxt-link to="/">
      Home page
    </nuxt-link>
  </div>
</template>

<script>
export default {
  layout: 'blog' // you can set a custom layout for the error page
}
</script>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  background-color: #fff;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  background-color: #fff;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

.button--light-green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #00C58E;
  background-color: #fff;
  color: #00C58E;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--light-green:hover {
  color: #fff;
  background-color: #00C58E;
}
</style>
