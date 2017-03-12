<template>
  <div id="app">
    <game-panel>
      <touch-block v-for="(styleObj,index) in blockColorArr" :colorStyle="styleObj" slot="blocks" :key="index" :keyNum="index + 1" :blingNum="blingNum" :eventHook="touchEventHook" :stopInput="stopInput" @creditTouch="getCreditInput"></touch-block>
      <operator-bar slot="operator" @startGame="startGame" @exitGame="exitGame" @repeatGame="showOrderToCredit" @strictModeChange="dealStrictMode"></operator-bar>
      <tester slot="tester" :checkPoint="checkPoint" :randomArr="randomArr" :creditArr="creditArr" :eventHook="testerEventHook" :eventHook2="testerEventHook2" @leavelUp="leavelUp" @testErr="showOrderToCredit" @testErrStrict="restartGame"></tester>
    </game-panel>
  </div>
</template>

<script type="text/ecmascript-6">
import gamePanel from './components/gamePanel/gamePanel'
import touchBlock from './components/touchBlock/touchBlock'
import operatorBar from './components/operatorBar/operatorBar'
import tester from './components/tester/tester'

export default {
  name: 'app',
  components: {
    'game-panel': gamePanel,
    'touch-block': touchBlock,
    'operator-bar': operatorBar,
    'tester': tester
  },
  data() {
    return {
      checkPoint: 0,
      blingNum: 0,
      touchEventHook: 0,
      testerEventHook: 0,
      testerEventHook2: 0,
      stopInput: true,
      strictMode: false,
      randomArr: [],
      creditArr: [],
      blockColorArr: [
        { before: '#aa382e', after: '#f44336' },
        { before: '#338e3c', after: '#4caf50' },
        { before: '#1976d2', after: '#03a9f4' },
        { before: '#ff9800', after: '#ffeb3b' }
      ]
    }
  },
  methods: {
    // 处理子组件的事件
    startGame() {
      let randomNum = Math.floor(Math.random() * 4 + 1)
      this.randomArr.push(randomNum)
      this.checkPoint++
      this.showOrderToCredit()
    },
    exitGame() {
      this.checkPoint = 0
      this.randomArr = []
      this.stopInput = true
    },
    restartGame() {
      this.exitGame()
      this.leavelUp()
    },
    leavelUp() {
      let randomNum = Math.floor(Math.random() * 4 + 1)
      this.randomArr.push(randomNum)
      this.checkPoint++
      let self = this
      setTimeout(function() {
        self.showOrderToCredit()
      }, 1000)
    },
    getCreditInput(keyNum) {
      this.creditArr.push(keyNum)
    },
    dealStrictMode(strictMode) {
      this.strictMode = strictMode
    },
    // 一次完整的游戏流程
    showOrderToCredit() {
      let self = this
      let randomArr = this.randomArr
      // 开始遍历 randomArr ， 将随机序列展示给用户
      for (let i = 0; i < randomArr.length; i++) {
        setTimeout(function() {
          // 递交给 touchBlock, 使其亮起
          self.blingNum = randomArr[i]
          self.touchEventHook++
            // 时间间隔为 1.5s
        }, 1500 * i)
      }
      // 在展示结束后，用户才被允许输入
      setTimeout(function() {
        // 允许用户输入
        self.stopInput = false
          // 将用户序列置空
        self.creditArr = []
      }, 1500 * (randomArr.length - 1))
    }
  },
  watch: {
    // 监听 creditArr 用户序列
    creditArr: function() {
      // 当 用户序列 和 随机序列 的长度相等时，阻止输入，并递交给 tester 处理
      if (this.strictMode || this.creditArr.length >= this.randomArr.length) {
        if (this.creditArr.length >= this.randomArr.length) {
          // 阻止用户输入
          this.stopInput = true
            // 递交给 tester 处理
          this.testerEventHook++
            // 处于严格模式时
        } else {
          // 递交给 tester 处理
          this.testerEventHook2++
        }
      }
    }
  }
}

</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
#app
  display flex
  justify-content center
</style>
