<template>
  <table id="game-grid">
    <tr v-for="row in 3" :key="row - 1">
      <GameTile 
        v-for="col in 3"
        :row="row - 1" 
        :col="col - 1"
        :value="tiles[row-1][col-1]" 
        :key="col - 1" 
        @tile-clicked="recordTileClick">
      </GameTile>
    </tr>
  </table>
</template>

<script>

import GameTile from "@/components/GameTile.vue";

export default {
  name: "Gameboard",
  props: {
    msg: String
  },
  data() {
    return {
      currentTurn: 1,
      // initialized with 0s. The GameTile Component will read 0s as null values and won't display anything
      tiles: [
        ['0','0','0'],
        ['0','0','0'],
        ['0','0','0'],
      ]
    }
  },
  methods: {
    recordTileClick(row, col){
      console.log('row is: ' + row);
      console.log('col is: ' + col);
    }
  },
  components: {
    GameTile
  }
};
</script>
<style>
  #game-grid{
    height: 350px;
    width: 350px;
    /* display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 100px 100px 100px;
    grid-column-gap: 5px;
    grid-row-gap: 5px;*/
    background-color: lemonchiffon;
    border: 5px gold solid; 
  }
  .game-tile{
    font-size: 30px;
    background-color: navy;
    height: 100px;
    width: 100px;
    vertical-align: middle;
    color: white;
  }
</style>

