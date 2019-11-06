<template>
  <div id="app">
    <Dpuzzle
      v-bind="PuzzleConfig[level]"
      @next='handleNext'
    >
    </Dpuzzle>
    <div>
      {{title}}
    </div>
  </div>
</template>

<script>
import Dpuzzle from './components/Puzzle.vue'
export default {
  name: 'app',
  components: {
    Dpuzzle
  },
  data() {
    return {
      title: '拼图小游戏',
      level: 0,
      PuzzleConfig: [
        { row: 3, col: 3, img: './images/pingtu1.jpg' },
        { row: 4, col: 4, img: './images/pingtu2.jpg' },
        { row: 5, col: 5, img: './images/pingtu3.jpg' },
        { row: 6, col: 6, img: './images/pingtu3.jpg' }
      ]
    }
  },
  methods: {
    handleNext() {
      if (++this.level == this.PuzzleConfig.length) {
        const anwerFlag = window.confirm('已经是最后一关了，要重新开始不？')
        if (anwerFlag) {
          this.level = 0
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
