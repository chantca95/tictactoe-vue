<template>
  <table id="game-grid">
    <div class="game-tile"></div>
    <div class="game-tile"></div>
    <div class="game-tile"></div>
    <div class="game-tile"></div>
    <div class="game-tile"></div>
    <div class="game-tile"></div>
    <div class="game-tile"></div>
    <div class="game-tile"></div>
    <div class="game-tile"></div>
  </table>
</template>

<script>
export default {
  name: "Gameboard",
  props: {
    msg: String
  },
  data() {
    return {
      currentTurn: 0,
    }
  }
};
</script>
<style scoped>
  #game-grid{
    display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 100px 100px 100px;
    grid-column-gap: 5px;
    grid-row-gap: 5px;
    background-color: lemonchiffon;
    border: 5px lemonchiffon solid;
  }
  .game-tile{
    font-size: 30px;
    background-color: navy;
    line-height: 100px;
    vertical-align: middle;
    color: white;
  }
</style>

