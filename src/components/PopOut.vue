<template>
  <div class="backdrop">
    <div class="modal">
      <h2 class="title">
        <span v-if="win">🎉 Bravo !</span>
        <span v-else>😢 Perdu</span>
      </h2>

      <p class="text">
        <span v-if="win">Tu as trouvé le mot :</span>
        <span v-else>Le mot était :</span>
        <strong class="word">{{ solution }}</strong>
      </p>

      <button class="btn" @click="$emit('restart')">Rejouer</button>
      <button class="btn ghost" @click="$emit('close')">Fermer</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    win: {
      type: Boolean,
      required: true,
    },
    solution: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
.backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
  display: grid;
  place-items: center;
  z-index: 1000;
}

.modal {
  background: #1f2937;
  padding: 20px;
  border-radius: 12px;
  width: 320px;
  text-align: center;
  color: white;
}

.title {
  margin-bottom: 10px;
}

.text {
  margin-bottom: 15px;
}

.word {
  margin-left: 6px;
  letter-spacing: 2px;
}

.btn {
  width: 100%;
  padding: 10px;
  margin-top: 8px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

.btn {
  background: #22c55e;
  color: black;
}

.ghost {
  background: transparent;
  border: 1px solid #9ca3af;
  color: white;
}
</style>