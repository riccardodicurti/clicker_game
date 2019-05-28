<template>
  <div id="app">
  <p>
    <router-link to="/">Go to Index</router-link>
    <router-link to="/hello">Go to Hello</router-link>
  </p>
  <!-- route outlet -->
  <!-- component matched by the route will render here -->
  <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
    }
  }
}

</script>

<style>

  h1 {
    color: #444;
    text-align: center;
    font-weight: normal;
  }

</style>
