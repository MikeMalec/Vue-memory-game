<template>
  <div class="bg-light p-5 mt-2 mb-2 w-100">
    <h3>Difficulty:</h3>
    <div class="mt-3">
      <div class="radio">
        <label>
          <input type="radio" name="optradio" value="easy" v-model="difficulty" checked />Easy
        </label>
      </div>
      <div class="radio">
        <label>
          <input type="radio" name="optradio" value="hard" v-model="difficulty" />Hard
        </label>
      </div>
      <div class="radio disabled">
        <label>
          <input type="radio" name="optradio" value="hero" v-model="difficulty" />Hero
        </label>
      </div>
      <button type="button" class="btn btn-primary w-100 mt-1 mb-n4" @click="startGame">Start Game</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Menu",
  data() {
    return {
      difficulty: "easy"
    };
  },
  methods: {
    startGame() {
      this.$emit("startGame", this.difficulty);
    }
  }
};
</script>

<style>
</style>