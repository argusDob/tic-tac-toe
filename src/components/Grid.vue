<template>
  <div class="grid" :class="{ grid__disabled: isGameFinished }">
    <div
      class="grid__cell"
      :id="item"
      v-for="item in grid.row1"
      :key="item"
      v-on:click="onClick($event)"
    ></div>
    <div
      class="grid__cell"
      :id="item"
      v-for="item in grid.row2"
      :key="item"
      v-on:click="onClick($event)"
    ></div>
    <div
      class="grid__cell"
      :id="item"
      v-for="item in grid.row3"
      :key="item"
      v-on:click="onClick($event)"
    ></div>
  </div>
</template>

<script>
export default {
  name: "my-grid",
  props: {
    icon: {
      type: String,
    },
    isGameFinished: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      grid: {
        row1: [0, 1, 2],
        row2: [3, 4, 5],
        row3: [6, 7, 8],
      },
    };
  },
  methods: {
    onClick(e) {
      this.$emit("onCellClick", e.currentTarget.id);
      setTimeout(() => {
        e.target.className +=
          " grid__cell-" + this.icon + " grid__cell-disabled";
      }, 100);
    },
  },
};
</script>

<style lang="scss">
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  width: 300px;
  height: 300px;
  margin: 0 auto;
  border: 2px solid black;
  box-sizing: border-box;

  &__cell {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    border: 2px solid black;
  }

  &__cell-cross {
    background-image: url("../assets/cross_icon.svg");
  }

  &__cell-circle {
    background-image: url("../assets/circle_icon.svg");
  }

  &__cell-disabled,
  &__disabled {
    pointer-events: none;
  }
}
</style>
