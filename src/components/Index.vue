<template>
  <div id="index">

    <h1> clicker game </h1>

    <div class="row">
      <div class="col-md-2">
        </br>
      </div>

      <div class="col-md-4">
        <Clicker :gold="gold" :food="food" :stats="stats" @click="click" @buy_food="buy_food" />
      </div>
      <div class="col-md-4">
        <Upgrades :upgrades="upgrades" :gold="gold" @upgrade="upgrade" />
      </div>

      <div class="col-md-2">
        </br>
      </div>
    </div>
  </div>
</template>

<script>
  import Upgrades from './Upgrades.vue'
  import Clicker from './Clicker.vue'

  export default {
    name: 'Index',
    components: {
      Upgrades,
      Clicker
    },
    data () {
      return {
        gold: 1200,
        food: 100,
        upgrades: [
          { id: 0, name: 'Auto Clicker', lv: 0, tooltip: '+1 gold/s', base_price: 100 },
          { id: 1, name: 'Colonists', lv: 0, tooltip: '+10 gold/s -2 food/s', base_price: 200 },
          { id: 2, name: 'Mines', lv: 0, tooltip: 'colonist + ( colonist * mines * 2)', base_price: 1000 },
        ],
        stats: [
          { id: 0, name: 'undermine gold', value: 0, tooltip: ' gold/s'},
          { id: 1, name: 'food consumption', value: 0, tooltip: ' food/s'},
        ]
      }
    },
    mounted: function() {
      this.set_auto_clicker();
    },
    methods: {
      upgrade(payload) {
        this.gold -= payload.base_price;
        this.upgrades.find( upgrade => upgrade.id === payload.id ).lv += 1;
        this.update_stats();
      },
      click() {
        this.gold++;
      },
      buy_food() {
        if ( this.gold >= 25 ) {
            this.gold -= 25;
            this.food += 100;
        }
      },
      game_loop() {
        var auto_clicker = this.upgrades.find( upgrade => upgrade.id === 0 ).lv;
        var colonists = this.upgrades.find( upgrade => upgrade.id === 1 ).lv;
        var mines = this.upgrades.find( upgrade => upgrade.id === 2 ).lv;

        if ( this.food >= ( colonists * 2 ) ) {
          this.food -= ( colonists * 2);
          this.gold += ( colonists * 10 ) + ( colonists * 10 * mines * 2);
        }

        this.gold += auto_clicker * 1;
      },
      update_stats() {
        var auto_clicker = this.upgrades.find( upgrade => upgrade.id === 0 ).lv;
        var colonists = this.upgrades.find( upgrade => upgrade.id === 1 ).lv;
        var mines = this.upgrades.find( upgrade => upgrade.id === 2 ).lv;

        this.stats.find( upgrade => upgrade.id === 0 ).value = auto_clicker + ( colonists * 10 ) + ( colonists * 10 * mines * 2);
        this.stats.find( upgrade => upgrade.id === 1 ).value = colonists * 2;
      },
      set_auto_clicker() {
          setInterval(this.game_loop, 1000);
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

  h1 {
    margin-bottom: 40px;
  }

  button[disabled], html input[disabled] {
      opacity: 0.4;
  }

</style>
