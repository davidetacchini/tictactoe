<template>
  <div class="board">
    <div v-for="x in 3" :key="x" class="board-row">
      <div
        v-for="y in 3"
        :key="computeIndex(x, y)"
        :class="[boxes[computeIndex(x, y)], 'board-box']"
        @click="$emit('update-box', computeIndex(x, y))"
      >
        {{ boxes[computeIndex(x, y)] }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Board",

  props: {
    boxes: Array,
  },

  setup() {
    const computeIndex = (x, y) => {
      return x * 3 + y - (3 + 1);
    };

    return { computeIndex };
  },
};
</script>

<style scoped>
.board {
  width: 40vh;
  height: 40vh;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: repeat(3, 1fr);
  grid-gap: 1rem;
  margin-block: 2rem;
}

.board-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 1fr;
  grid-gap: 1rem;
}

/* box-shadow: 0 0 8px rgba(0, 0, 0, 0.101562); */
.board-box {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: var(--border-radius-1);
  font-size: 3rem;
  box-shadow: var(--box-shadow);
  cursor: pointer;
  overflow: hidden;
  transition: background-color 50ms ease, box-shadow 50ms ease, transform 50ms linear;
}

.board-box.X {
  color: var(--player-x);
}

.board-box.O {
  color: var(--player-o);
}

.board-box:hover {
  background-color: var(--background-beta);
}

.board-box:focus,
.board-box:active {
  --box-shadow: 0 0 16px rgb(69, 69, 79);
  box-shadow: var(--box-shadow);
  transform: scale(1.05);
}
</style>
