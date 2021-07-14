<template>
  <div class="game">
    <h1>
      Next: <span :class="playerColor(player)">{{ player }}</span>
    </h1>
    <board :boxes="boxes" @update-box="update" />
  </div>
  <cheering v-if="winner !== null" :winner="winner" @play-again="restart" />
</template>

<script>
import { computed, ref } from "vue";
import { playerColor } from "../common/utils.js";
import { confetti } from "dom-confetti";
import Board from "./Board";
import Cheering from "./Cheering";

export default {
  name: "Game",

  components: {
    Board,
    Cheering,
  },

  setup() {
    const boxes = ref(Array(9).fill(null));
    const player = ref("X");
    const moves = ref(0);
    const winner = computed(() => computeWinner(boxes.value));

    const computeWinner = (boxes) => {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (boxes[a] && boxes[a] === boxes[b] && boxes[a] === boxes[c]) {
          // shows amazing confetti everywhere cause you deserve it
          const app = document.querySelector("#app");
          confetti(app, { duration: 2000 });
          return boxes[a];
        }
      }
      if (moves.value === boxes.length) {
        // return undefined if it's a draw
        return;
      } else {
        return null;
      }
    };

    const update = (index) => {
      if (boxes.value[index] || computeWinner(boxes.value)) return;
      boxes.value[index] = player.value;
      moves.value++;
      player.value = player.value === "O" ? "X" : "O";
    };

    const restart = () => {
      boxes.value = Array(9).fill(null);
      player.value = "X";
      moves.value = 0;
    };

    return {
      boxes,
      player,
      winner,
      playerColor,
      update,
      restart,
    };
  },
};
</script>

<style scoped>
.game {
  text-align: center;
}

.player-x {
  color: var(--player-x);
}

.player-o {
  color: var(--player-o);
}
</style>
