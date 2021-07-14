<template>
  <div class="cheering">
    <div class="container">
      <h1 v-if="winner === undefined">Draw!</h1>
      <h1 v-else>
        <span :class="playerColor(winner)">{{ winner }}</span> won!
      </h1>
      <div class="button" @click="$emit('play-again')">Play Again</div>
    </div>
  </div>
</template>

<script>
import { playerColor } from "../common/utils.js";

export default {
  name: "Cheering",

  props: {
    winner: String,
  },

  setup() {
    return { playerColor };
  },
};
</script>

<style scoped>
.cheering {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  background-color: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
}

.container {
  height: 80%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

h1 {
  font-size: 4rem;
}

.button {
  border-radius: var(--border-radius-1);
  background-color: var(--button-alpha);
  width: fit-content;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  cursor: pointer;
  user-select: none;
}
</style>
