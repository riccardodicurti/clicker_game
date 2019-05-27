<template>
  <div id="index">
    <h1> Lemonade stand </h1>
    <div class="row">
      <div class="col-md-2">
        </br>
      </div>
      <div class="col-md-4">
        <Clicker :gold="gold" :food="food" :stats="stats" :other="other" @click="click" @buy_food="buy_food" />
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
        gold: 1000,
        food: 100,
        multiplier: 1.15, 
        upgrades: [
          { id: 0, name: 'Auto Clicker', lv: 0, tooltip: '+1 gold/s', price: 100 },
          { id: 1, name: 'Colonists', lv: 0, tooltip: '+10 gold/s -2 food/s', price: 200 },
          { id: 2, name: 'Mines', lv: 0, tooltip: 'colonist + ( colonist * mines * 2)', price: 1000 }       
        ],
        stats: [
          { id: 0, name: 'undermine gold', value: 0, tooltip: ' gold/s'},
          { id: 1, name: 'food consumption', value: 0, tooltip: ' food/s'}
        ],
        other: [
          { id: 0, name: 'food', lv: 0, tooltip: ' buy food at the general store', price: 25},
        ]
      }
    },
    mounted: function() {
      this.set_auto_clicker();
    },
    methods: {
      upgrade(payload) {
        this.gold -= payload.price;
        
        var price = this.upgrades.find( upgrade => upgrade.id === payload.id ).price;
        var lv = this.upgrades.find( upgrade => upgrade.id === payload.id ).lv;     
                
        this.upgrades.find( upgrade => upgrade.id === payload.id ).lv += 1;      
        this.upgrades.find( upgrade => upgrade.id === payload.id ).price = Math.round( price * Math.pow(this.multiplier, lv) );     
      },
      click() {
        this.gold++;
      },
      buy_food(payload) {
          this.gold -= this.other[0].price;
          this.food += this.other[0].price + 25;
          this.other[0].lv += 1;
          this.other[0].price = Math.round( this.other[0].price * Math.pow(this.multiplier, this.other[0].lv) );
      },
      game_loop() {
        var auto_clicker = this.upgrades.find( upgrade => upgrade.id === 0 ).lv;
        var colonists = this.upgrades.find( upgrade => upgrade.id === 1 ).lv;
        var mines = this.upgrades.find( upgrade => upgrade.id === 2 ).lv; 
        var undermine_gold = auto_clicker * 1;
        var food_consumption = 0; 
        if ( this.food >= ( colonists * 2 ) ) {
          food_consumption = ( colonists * 2);
          undermine_gold += ( colonists * 10 ) + ( colonists * 10 * mines * 2);
        }
        this.gold += undermine_gold;
        this.food -= food_consumption;                  
        this.stats.find( upgrade => upgrade.id === 0 ).value = undermine_gold;
        this.stats.find( upgrade => upgrade.id === 1 ).value = food_consumption;
      },
      set_auto_clicker() {
          setInterval(this.game_loop, 1000);
      }
    }
  }
</script>

<style>
  
</style>
