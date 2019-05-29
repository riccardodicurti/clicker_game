<template>
  <div id="app">  
    <ul class="nav nav-tabs">
      <li class="nav-item">
        <router-link to="/">Game</router-link>
      </li>
      <li class="nav-item">
        <router-link to="/settings">Settings</router-link>
      </li>
    </ul>  
    
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
