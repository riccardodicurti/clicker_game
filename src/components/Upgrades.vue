<template>

  <div id="potenziamenti">

    <div v-for="( u ) in upgrades" :key="u.id">
      [ lv: {{ u.lv }} ]: <button class="" @click="upgrade(u.id, u.price)" :disabled="gold < u.price"> {{ u.price }} - {{ u.name }} </button> {{ u.tooltip }}
    </div>

  </div>

</template>

<script>

export default {
  name: 'Upgrades',
  props: ['upgrades', 'gold'],
  data () {
    return {

    }
  },
  methods: {
    upgrade(id, price) {
      this.$emit('upgrade', { id, price })
    }
  }
}

</script>

<style>

</style>
