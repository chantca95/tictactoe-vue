<template>
  <td v-on:click="tileClicked" class="game-tile">{{ value === "0" ? '' : value }}</td>
</template>

<script>
export default {
  name: "Gameboard",
  props: {
    row: Number,
    col: Number,
    value: String,
  },
  methods: {
    tileClicked() {
      console.log('tile response: ' + this.row + ' ' + this.col)
      this.$emit('tile-clicked', this.row, this.col,);
    }
  }
}
</script>
