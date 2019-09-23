<template>
  <div class="home">
    <img alt="Tic Tac Toe logo" src="../assets/tictactoe.jpeg" />
    <div class="hello">
      <h1>{{ msg }}</h1>
    <div class="column-group">
      <Gameboard v-if="gameHasStarted" ></Gameboard>
      <div @mousedown="startGame" v-else id="start-button">Start</div>      
    </div>
  </div>
  </div>
</template>

<script>
// @ is an alias to /src
// you import components that you're going to use in your Home.vue page
import Gameboard from "@/components/Gameboard.vue";

export default {
  name: "home",
  data() {
    return {
      msg: "Welcome to Tic Tac Toe",
      gameHasStarted: false
    }
  },
  methods: {
    startGame() {
      this.gameHasStarted = true;
    }
  },
  components: {
    Gameboard
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#start-button, #restart-button {
  font-size: 20px;
  width: 100px;
  padding: 10px;
  margin: 20px 0px;
  text-align: middle;
  background-color: navy;
  color: white;
}
.column-group {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
