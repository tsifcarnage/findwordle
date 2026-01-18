<script>
export default {
  name: "keyBoard",
  emits: ["submit-word", "key-press"],
  props: {
    keyboardStatus: {
      type: Object,
      default: () => ({}),
    },
  },

  data() {
    return {
      typedWord: [],
      keyboard: [
        ["A", "Z", "E", "R", "T", "Y", "U", "I", "O", "P"],
        ["Q", "S", "D", "F", "G", "H", "J", "K", "L"],
        ["ENTER", "W", "X", "C", "V", "B", "N", "M", "DEL"],
      ],
    };
  },
  methods: {
    pressKey(key) {
      this.$emit("key-press", key);

      if (key === "DEL") {
        this.typedWord.pop();
      } else if (key === "ENTER") {
        if (this.typedWord.length === 5) {
          this.$emit("submit-word", this.typedWord.join(""));
          this.typedWord = [];
        }
      } else if (this.typedWord.length < 5) {
        this.typedWord.push(key);
      }
    },

    keyClass(key) {
      if (key === "ENTER" || key === "DEL") {
        return "bg-gray-500 hover:bg-gray-400 flex-1";
      }

      const status = this.keyboardStatus[key];

      return (
        {
          correct: "bg-green-600",
          present: "bg-yellow-500",
          absent: "bg-red-500",
        }[status] || "bg-gray-600 hover:bg-gray-500"
      );
    },
  },
};
</script>
<template>
  <section class="flex flex-col gap-1 mt-6 px-2 max-w-[480px] mx-auto">
    <div
      v-for="(row, index) in keyboard"
      :key="index"
      class="flex justify-center gap-1.5"
    >
      <button
        v-for="key in row"
        :key="key"
        @click="pressKey(key)"
        :class="[
          'px-3 sm:px-4 py-3.5 sm:py-4 rounded font-bold text-white text-base sm:text-lg transition-colors',
          'min-h-[52px]',
          'active:scale-[0.97]',
          'touch-manipulation select-none',
          key === 'ENTER' || key === 'DEL'
            ? 'min-w-[70px] sm:min-w-[90px] text-sm'
            : 'flex-1 max-w-11 sm:max-w-[52px]',
          keyClass(key),
        ]"
      >
        {{ key }}
      </button>
    </div>
  </section>
</template>
<script scoped></script>
