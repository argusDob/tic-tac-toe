<template>
  <div id="app">
    <Grid :icon="icon" 
    :isGameFinished="isGameFinished"
    @onCellClick="onCellClick" />
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
      board: [" ", " ", " ", " ", " ", " ", " ", " ", " "],
      icon: "cross",
      isGameFinished: false,
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
      console.log(this.checkWinner());
      if (this.checkWinner()) {
        console.log("The winner is:", this.currentPlayer);
        this.isGameFinished = true
      } 
      if (this.checkWinner() === "draw") {
        this.isGameFinished = true
        console.log("DRAW");
      }
    },
    setupIcon() {
      this.icon = this.currentPlayer === "O" ? "circle" : "cross";
    },
    updateBoard(cellId) {
      this.board[cellId] = this.currentPlayer;
    },
    checkWinner() {
      // check for a draw
      if (this.board.every((cell) => cell != " ") && !this.hasWinner()) {
        return "draw";
      }

      // check for a winner
      if (this.hasWinner()) {
        return true;
      }

      return false;
    },
    hasWinner() {
      const winningCombinations = this.getWinningCombinationsDefinition();

      // loop through winning combinations and check for a winner
      for (let comb of winningCombinations) {
        if (
          this.board[comb[0]] == this.board[comb[1]] &&
          this.board[comb[1]] == this.board[comb[2]] &&
          this.board[comb[0]] != " "
        ) {
          return true;
        }
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
