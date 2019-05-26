<template>

  <div id="potenziamenti">

    <div v-for="( u ) in upgrades" :key="u.id">
      [ lv: {{ u.lv }} ]: <button class="" @click="upgrade(u.id, u.base_price)" :disabled="gold < u.base_price"> {{ u.base_price }} {{ u.name }} </button> {{ u.tooltip }}
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
    upgrade(id, base_price) {
      this.$emit('upgrade', { id, base_price })
    }
  }
}

</script>

<style>

</style>
