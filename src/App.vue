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
      board: [" ", " ", " ", " ", " ", " ", " ", " ", " "],
      OPlayer: "O",
      XPlayer: "X",
    };
  },
  methods: {
    onCellClick(id) {
      this.currentPlayer =
        this.currentPlayer === this.OPlayer ? this.XPlayer : this.OPlayer;
      this.setupIcon();
      this.updateBoard(id);
      if (this.checkWinner()) {
        console.log(this.currentPlayer);
      } else if (this.checkWinner() === 'draw'){
        console.log("DRAW")
      }
    },
    setupIcon() {
      this.icon = this.currentPlayer === "O" ? "circle" : "cross";
    },
    updateBoard(cellId) {
      this.board[cellId] = this.currentPlayer;
    },
    checkWinner() {
      const winningCombinations = this.getWinningCombinationsDefinition();
      for (let comb of winningCombinations) {
        if (
          this.board[comb[0]] == this.board[comb[1]] &&
          this.board[comb[1]] == this.board[comb[2]] &&
          this.board[comb[0]] != " "
        ) {
          return true;
        }
      }
      if (this.board.every((cell) => cell != " ")) {
          return "draw";
        }
      return false;
    },
    getWinningCombinationsDefinition() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8], // horizontal
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8], // vertical
        [0, 4, 8],
        [2, 4, 6], // diagonal
      ];

      return winningCombinations;
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
