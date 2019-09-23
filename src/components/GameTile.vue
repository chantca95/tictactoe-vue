<template>
  <td v-on:click="tileClicked" class="game-tile">{{ value === '0' ? '' : value }}</td>
</template>

<script>
export default {
  name: "Gameboard",
  props: {
    id: Number,
    value: String,
  },
  methods: {
    tileClicked() {
      console.log('tile response: ' + this.id)
      this.$emit('tile-clicked', this.id);
    }
  },
}
</script>
