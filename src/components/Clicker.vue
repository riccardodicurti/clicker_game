<template>

  <div id="clicker">
    <span>{{ stats[0].name }}: {{ stats[0].value }} {{ stats[0].tooltip }}</span></br>
    <span>{{ stats[1].name }}: {{ stats[1].value }} {{ stats[1].tooltip }}</span></br>
    </br>
    <span>gold reserves: {{ gold }}</span></br>
    <span>food reserves: {{ food }}</span></br>
    </br>
    <button @click="click()" alt="make oro"> undermine gold </button></br>
    <button @click="buy_food()" alt="buy food" :disabled="gold < other[0].price"> {{ other[0].price }} - {{ other[0].tooltip }} </button>
  </div>

</template>

<script>

export default {
  name: 'Clicker',
  props: ['gold', 'food', 'stats', 'other'],
  data () {
    return {

    }
  },
  methods: {
    click() {
      this.$emit( 'click', { } )
    },
    buy_food() {
      this.$emit( 'buy_food', { } )
    }
  }
}

</script>

<style>

</style>
