<template>
  <div class="container border mt-5">
    <div class="d-flex justify-content-center" v-if="!play">
      <Menu @startGame="startGame" v-if="!gameEnded" />
      <Result :clicks="clicks" :startTime="startTime" :endTime="endTime" @newGame="newGame" v-else />
    </div>
    <div class="d-flex flex-wrap mt-3 mb-5 mt-5 ml-5 mr-5" v-else>
      <Tile
        v-for="tile in tiles"
        :key="tile.id"
        :tile="tile"
        :bothFilled="bothFilled"
        @setTile="setTile"
      />
    </div>
    <div class="d-flex flex-row-reverse bd-highlight" v-if="play">
      <button type="button" class="btn btn-primary mb-2 mt-2" @click="newGame">New Game</button>
    </div>
  </div>
</template>

<script>
import Menu from "./components/Menu";
import Result from "./components/Result";
import Tile from "./components/Tile";
export default {
  name: "app",
  components: {
    Menu,
    Tile,
    Result
  },
  data() {
    return {
      play: false,
      gameEnded: false,
      startTime: null,
      endTime: null,
      tiles: [],
      clicks: 0,
      firstTileValue: null,
      secondTileValue: null,
      bothFilled: false
    };
  },
  methods: {
    startGame(difficulty) {
      this.startTime = new Date().getTime();
      this.tiles = [];
      let amountOfTiles;
      if (difficulty === "easy") {
        amountOfTiles = 10;
      } else if (difficulty === "hard") {
        amountOfTiles = 20;
      } else {
        amountOfTiles = 30;
      }
      for (let i = 0; i < amountOfTiles; i++) {
        this.tiles.push({ id: i, value: i, active: false, founded: false });
      }
      for (let j = amountOfTiles; j < amountOfTiles * 2; j++) {
        this.tiles.push({
          id: j,
          value: j - amountOfTiles,
          active: false,
          founded: false
        });
      }
      this.shuffleTiles(this.tiles);
      this.play = true;
    },
    checkWhetherEndGame() {
      const stillPlaying = this.tiles.some(tile => tile.founded === false);
      if (!stillPlaying) {
        this.play = false;
        this.gameEnded = true;
        this.endTime = new Date().getTime();
      }
    },
    newGame() {
      this.play = false;
      this.gameEnded = false;
    },
    clearState() {
      this.firstTileValue = null;
      this.secondTileValue = null;
    },
    checkCurrentTiles() {
      if (this.firstTileValue !== null && this.secondTileValue !== null) {
        if (this.firstTileValue === this.secondTileValue) {
          this.tiles.forEach(tile => {
            if (tile.value === this.firstTileValue) {
              tile.founded = true;
            }
          });
        }
        setTimeout(() => {
          this.tiles.forEach(tile => (tile.active = false));
          this.clearState();
          this.bothFilled = false;
        }, 350);
        this.checkWhetherEndGame();
      }
    },
    setTile(value) {
      this.clicks++;
      if (this.firstTileValue === null) {
        this.firstTileValue = value;
      } else {
        this.bothFilled = true;
        this.secondTileValue = value;
      }
      this.checkCurrentTiles();
    },
    shuffleTiles(tiles) {
      for (let i = tiles.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [tiles[i], tiles[j]] = [tiles[j], tiles[i]];
      }
    }
  }
};
</script>

<style>
</style>
