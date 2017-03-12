<template>
  <div class="touch-block" :style="{backgroundColor: blockColor}" @click="creditInput"></div>
</template>

<script type="text/ecmascript-6">
export default {
  props: {
    'colorStyle': {
      type: Object
    },
    'keyNum': {
      type: Number
    },
    'blingNum': {
      type: Number
    },
    'eventHook': {
      type: Number
    },
    'stopInput': {
      type: Boolean
    }
  },
  data() {
    return {
      blockColor: ''
    }
  },
  created() {
    this.blockColor = this.colorStyle.before
  },
  methods: {
    // emitEvent 表示是否允许发射事件
    bling(emitEvent) {
      this.blockColor = this.colorStyle.after
      setTimeout(() => {
        this.blockColor = this.colorStyle.before
        if (emitEvent) {
          this.$emit('creditTouch', this.keyNum)
        }
      }, 1000)
      // 亮起到恢复的时长为1.4s
    },
    creditInput() {
      if (this.stopInput) {
        return
      }
      this.bling(true)
    }
  },
  watch: {
    // 依靠 eventHook 从父组件触发 bling
    eventHook: function() {
      if (this.keyNum === this.blingNum) {
        this.bling(false)
      }
    }
  }
}

</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
.touch-block
  width 225px
  height 225px
  transition 0.4s
</style>
