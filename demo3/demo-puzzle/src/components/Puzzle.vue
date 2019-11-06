<template>
  <div
    class="puzzle"
    :style="{width:width+'px',height:height+'px'}"
  >
    <div
      class="puzzle__block"
      v-for="(item,index) in blockPoints"
      :key="item.id"
      :style="{
        width:blockWidth+'px',height:blockHeight+'px',
        left:item.x+'px',
        top:item.y+'px',
        backgroundImage:`url(${img})`,
        backgroundPosition:`-${correctPoints[index].x}px -${correctPoints[index].y}px`,
        opacity:index===blockPoints.length-1&&0
      }"
      @click="handleClick"
      :ref="index===blockPoints.length-1?'empty':'block'"
      :data-correctX='correctPoints[index].x'
      :data-correctY='correctPoints[index].y'
    ></div>
  </div>

</template>
<script>
export default {
  props: {
    width: {
      type: Number,
      default: 500
    },
    height: {
      type: Number,
      default: 500
    },
    row: {
      type: Number,
      default: 3
    },
    col: {
      type: Number,
      default: 3
    },
    img: {
      type: String,
      required: true
    }
  },
  computed: {
    blockWidth() {
      return this.width / this.col
    },
    blockHeight() {
      return this.height / this.row
    },
    correctPoints() {
      const { row, col, blockWidth, blockHeight } = this
      const arr = []
      for (let i = 0; i < row; i++) {
        for (let j = 0; j < col; j++) {
          arr.push({
            x: j * blockWidth,
            y: i * blockHeight,
            id: new Date().getTime() + Math.random() * 100
          })
        }
      }
      return arr
    },
    blockPoints() {
      const points = this.correctPoints
      const length = points.length
      const lastEle = points[length - 1]
      const newArr = [...points]
      newArr.length = length - 1
      newArr.sort(() => Math.random() - 0.5)
      newArr.push(lastEle)
      return newArr
    }
  },
  methods: {
    handleClick(e) {
      const blockDom = e.target
      const emptyDom = this.$refs.empty[0]
      if (!this.isAdjacent(blockDom, emptyDom)) {
        return
      }
      const { left, top } = blockDom.style
      blockDom.style.left = emptyDom.style.left
      blockDom.style.top = emptyDom.style.top
      emptyDom.style.left = left
      emptyDom.style.top = top
      const flag = this.checkWin()
      if (flag) {
        this.winGame(emptyDom)
      }
    },
    isAdjacent(blockDom, emptyDom) {
      parseInt
      const { left: blockLeft, top: blockTop, width, height } = blockDom.style
      const { left: emptyLeft, top: emptyTop } = emptyDom.style
      const xDis = Math.floor(
        Math.abs(parseFloat(blockLeft) - parseFloat(emptyLeft))
      )
      const yDis = Math.floor(
        Math.abs(parseFloat(blockTop) - parseFloat(emptyTop))
      )
      const flag =
        (blockTop === emptyTop && xDis == parseInt(height)) ||
        (blockLeft === emptyLeft && yDis === parseInt(width))
      return flag
    },
    checkWin() {
      const blockDomArr = this.$refs.block
      return blockDomArr.every(dom => {
        const { left: domLeft, top: domTop } = dom.style
        const { correctx: correctX, correcty: correctY } = dom.dataset
        const flag =
          parseInt(domLeft) === parseInt(correctX) &&
          parseInt(domTop) === parseInt(correctY)
        return flag
      })
    },
    winGame(emptyDom) {
      emptyDom.style.opacity = 1
      setTimeout(() => {
        alert('拼图成功，恭喜！')
        setTimeout(() => {
          this.goToNextLevel()
        }, 300)
      }, 300)
    },
    goToNextLevel() {
      const answerFlag = window.confirm('要玩下一关吗？')
      if (answerFlag) {
        this.$emit('next')
      }
    }
  }
}
</script>

<style >
.puzzle {
  border: 2px solid #ccc;
  position: relative;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}
.puzzle__block {
  position: absolute;
  box-sizing: border-box;
  border: 1px solid #fff;
  transition: all 0.3s;
}
</style>