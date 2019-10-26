<template>
  <div class="card w-25" :class="{'alert-success' : founded}" style="height:50px" @click="setCard">
    <div class="card-body">
      <div v-if="founded"></div>
      <div v-else>
        <h3 class="text-center mt-n2" v-if="tile.active == true">{{tile.value}}</h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tile: {
      type: Object
    },
    bothFilled: {
      type: Boolean
    }
  },
  computed: {
    founded() {
      return this.tile.founded;
    }
  },
  methods: {
    setCard() {
      if (
        !this.tile.active &&
        this.founded === false &&
        this.bothFilled == false
      ) {
        this.tile.active = true;
        this.$emit("setTile", this.tile.value);
      }
    }
  }
};
</script>

<style>
</style>