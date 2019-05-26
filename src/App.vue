<template>
  <div id="app">
    <Index />
  </div>
</template>

<script>

import Index from './components/Index.vue'

export default {
  name: 'App',
  components: {
    Index
  },
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
