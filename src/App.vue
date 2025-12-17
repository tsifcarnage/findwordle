<script>
import Nav from "./components/Nav.vue";
import APIGet from "./components/APIGet.vue";
import GameBoard from "./components/GameBoard.vue";

export default {
  components: {
    Nav,
    APIGet,
    GameBoard,
  },

  data() {
    return {
      // mot secret venant de l'API (travail de ton ami)
      secretWord: "",

      // état du jeu
      currentRow: 0,
      currentCol: 0,
      maxRows: 6,
      wordLength: 5,
      gameOver: false,

      // grille Wordle 6x5
      board: Array.from({length: 6}, () =>
          Array.from({length: 5}, () => ({
            letter: "",
            status: "", // correct | present | absent
          }))
      ),
    };
  },

  methods: {
    // 🔑 IMPORTANT : lien avec APIGet.vue (À NE PAS SUPPRIMER)
    onWordReady(word) {
      this.secretWord = word.toUpperCase();
      console.log("Mot secret récupéré :", this.secretWord);
    },
  },
};
</script>

<template>
  <div class="app">
    <!-- Nav faite par ton ami -->
    <Nav/>

    <!-- API faite par ton ami -->
    <APIGet @word-ready="onWordReady"/>

    <!-- Grille du jeu (ton travail commence ici) -->
    <GameBoard :board="board"/>
  </div>
</template>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
</style>