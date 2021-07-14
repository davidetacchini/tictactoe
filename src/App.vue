<template>
  <game />
</template>

<script>
import Game from "./components/Game";

export default {
  name: "App",

  components: {
    Game,
  },
};
</script>

<style>
:root {
  --background-alpha: rgb(33, 33, 33);
  --background-beta: rgb(60, 60, 68);
  --text-alpha: rgb(229, 229, 233);
  --button-alpha: rgb(57, 132, 255);
  --border-radius-1: 1rem;
  --box-shadow: 0 0 8px rgb(69, 69, 79);
  --player-x: rgb(255, 123, 114);
  --player-o: rgb(126, 231, 135);
}

body {
  font-family: "Avenir", sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  min-width: 320px;
  background-color: var(--background-alpha);
  color: var(--text-alpha);
}

#app {
  height: 80vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.player-x {
  color: var(--player-x);
}

.player-o {
  color: var(--player-o);
}
</style>
