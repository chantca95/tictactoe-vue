<template>
<div class="gameboard-wrapper">
  <div id="game-grid">
    <GameTile v-for="tile in tiles"
      :key = tile.id
      :id = tile.id
      :value = tile.value
      @tile-clicked="recordTileClick"
    ></GameTile>
  </div>
  <div class="status-message">{{ statusMsg }}</div>
  <div @mousedown="resetGame" id="restart-button">Restart</div>
</div>
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
      status: 'playerTurn',
      currentTurn: 1,
      // initialized with 0s. The GameTile Component will read 0s as null values and won't display anything
      tiles: [
      ],
      playerToSymbolMap: {
        1 : 'O',
        2 : 'X'
      }
    }
  },
  methods: {
    recordTileClick(index){
      if (this.status === "winState") {
        return;
      }
      if (this.tiles[index].value !== '0') {
        this.printInvalidMoveBanner();
        return;
      }
      let symbol = this.playerToSymbolMap[this.currentTurn];
      this.tiles[index].value = symbol;
      if (this.winStateReached(index, symbol) === true) {
        this.printWinBanner();
        return;
      }
      this.changePlayer();
    },
    changePlayer(){
      if (this.currentTurn === 1) {
        this.currentTurn = 2;
      } else {
        this.currentTurn = 1;
      }
    },
    printInvalidMoveBanner() {
      this.status = 'invalidMove'
    },
    printWinBanner() {
      this.status = 'winState'
    },
    winStateReached(index, symbol) {
      let row = parseInt(index / 3);
      let col = index % 3;
      if (
        this.horizontalWin(row, col, symbol) === true ||
        this.verticalWin(row, col, symbol) === true ||
        this.diagonalWinTopLeftBotRight(row, col, symbol) === true ||
        this.diagonalWinBotLeftTopRight(row, col, symbol) === true
      ) {
        return true;
      }
    },
    horizontalWin(row, col, symbol) {
      let consecutiveCounter = 0;
      for (let i = - 2; i < 3; i++) {
        if (col + i < 0 || col + i > 2) {
          continue;
        }
        if (this.tiles[row * 3 + col + i].value === symbol) {
          consecutiveCounter++;
        }
        if (consecutiveCounter === 3) {
          return true;
        }
      }
      return false;
    },
    verticalWin(row, col, symbol) {
      let consecutiveCounter = 0;
      for (let i = - 2; i < 3; i++) {
        if (row + i < 0 || row + i > 2) {
          continue;
        }
        if (this.tiles[(row + i) * 3 + col].value === symbol) {
          consecutiveCounter++;
        }
        if (consecutiveCounter === 3) {
          return true;
        }
      }
      return false;
    },
    diagonalWinTopLeftBotRight(row, col, symbol) {
      let consecutiveCounter = 0;
      for (let i = - 2; i < 3; i++) {
        if (row + i < 0 || row + i > 2 || col + i < 0 || col + i > 2) {
          continue;
        }
        if (this.tiles[(row + i) * 3 + col + i].value === symbol) {
          consecutiveCounter++;
        }
        if (consecutiveCounter === 3) {
          return true;
        }
      }
      return false;
    },
    diagonalWinBotLeftTopRight(row, col, symbol) {
      let consecutiveCounter = 0;
      for (let i = - 2; i < 3; i++) {
        if (row + i < 0 || row + i > 2 || col - i < 0 || col - i > 2) {
          continue;
        }
        if (this.tiles[(row + i) * 3 + col - i].value === symbol) {
          consecutiveCounter++;
        }
        if (consecutiveCounter === 3) {
          return true;
        }
      }
      return false;
    },
    resetGame(){
      this.tiles = [
        {id: 0, value: '0'},
        {id: 1, value: '0'},
        {id: 2, value: '0'},
        {id: 3, value: '0'},
        {id: 4, value: '0'},
        {id: 5, value: '0'},
        {id: 6, value: '0'},
        {id: 7, value: '0'},
        {id: 8, value: '0'},
      ]
      this.status = 'playerTurn';
    }
  },
  beforeMount() {
    this.resetGame();
  },
  components: {
    GameTile
  },
  computed: {
    statusMsg() {
      let playerTurnPhrase = "Player " + this.currentTurn + "'s turn!"
      if (this.status === 'playerTurn') {
        return playerTurnPhrase
      } else if (this.status === 'invalidMove') {
        let prefix = "Invalid Move. You may only click on unoccupied tiles. "
        return prefix + playerTurnPhrase
      } else {
        return "Player " + this.currentTurn + " wins! Click restart to start over!"
      }
    }
  }
};
</script>
<style>
  #game-grid{
    display: grid;
    width: 310px;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 100px 100px 100px;
    grid-column-gap: 5px;
    grid-row-gap: 5px;
    background-color: gold;
    border: 5px gold solid; 
  }
  .game-tile{
    font-size: 30px;
    background-color: navy;
    line-height: 100px;
    height: 100px;
    width: 100px;
    vertical-align: middle;
    color: white;
  }
  .status-message{
    font-size: 30px;
    color:darkgray;
    margin-top: 30px;
  }
  .gameboard-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>

