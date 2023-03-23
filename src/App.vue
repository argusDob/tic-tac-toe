<template>
  <div id="app">
    <Grid :icon="icon" @onCellClick="onCellClick" />
  </div>
</template>

<script>
import Grid from "./components/Grid.vue";

export default {
  name: "App",
  components: {
    Grid,
  },
  data() {
    return {
      icon: "cross",
      spaces: [],
      OPlayer: "O",
      XPlayer: "X",
    };
  },
  methods: {
    onCellClick(id) {
      this.setupIcon()
      
      if (!this.spaces[id]) {
        this.currentPlayer =
          this.currentPlayer === this.OPlayer ? this.XPlayer : this.OPlayer;
        this.spaces[id] = this.currentPlayer;
        if (this.playerWon(this.currentPlayer)) {
          console.log(this.currentPlayer);
        }
      }
    },
    setupIcon(){
      this.icon = (this.currentPlayer === "O") ? "circle" : "cross";
    },
    playerWon(player) {
      // console.log(this.spaces[0])
      if (this.spaces[0] === player) {
        if (this.spaces[1] === player && this.spaces[2] === player) return true;
        if (this.spaces[3] === player && this.spaces[6] === player) return true;
        if (this.spaces[4] === player && this.spaces[8] === player) return true;
      }
      if (this.spaces[8] === player) {
        if (this.spaces[2] === player && this.spaces[5] === player) return true;
        if (this.spaces[6] === player && this.spaces[7] === player) return true;
      }
      if (this.spaces[4] === player) {
        if (this.spaces[1] === player && this.spaces[7] === player) return true;
        if (this.spaces[3] === player && this.spaces[5] === player) return true;
        if (this.spaces[2] === player && this.spaces[6] === player) return true;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
