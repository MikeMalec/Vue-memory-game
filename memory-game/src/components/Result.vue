<template>
  <div class="bg-light w-100 p-t mt-5">
    <h3>Time: {{getTime}}</h3>
    <h3>Moves: {{getClicks}}</h3>
    <button type="button" class="btn btn-primary w-100 mt-1 mb-n4" @click="newGame">New Game</button>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: {
    clicks: {
      type: Number
    },
    startTime: {
      type: Number
    },
    endTime: {
      type: Number
    }
  },
  computed: {
    getTime() {
      const time = ((this.endTime - this.startTime) / 1000).toFixed(2);
      return `${time} seconds`;
    },
    getClicks() {
      return this.clicks / 2;
    }
  },
  methods: {
    newGame() {
      this.$emit("newGame");
    }
  }
};
</script>

<style>
</style>