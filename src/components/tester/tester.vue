<template>
  <div class="tester">{{ checkPointText }}</div>
</template>

<script type="text/ecmascript-6">
export default {
  props: {
    'randomArr': {
      type: Array
    },
    'creditArr': {
      type: Array
    },
    'checkPoint': {
      type: Number
    },
    'eventHook': {
      type: Number
    },
    'eventHook2': {
      type: Number
    }
  },
  data() {
    return {
      log: undefined
    }
  },
  computed: {
    checkPointText() {
      if (this.checkPoint < 1) {
        return '--'
      }
      if (this.log) {
        return this.log
      }
      if (this.checkPoint >= 20) {
        return 'WIN'
      }
      return this.checkPoint
    }
  },
  watch: {
    eventHook: function() {
      let self = this
      for (let i = 0; i <= this.creditArr.length; i++) {
        if (this.randomArr[i] !== this.creditArr[i]) {
          this.$emit('testErr')
          this.log = 'ERR'
          setTimeout(function() {
            self.log = undefined
          }, 1000)
          return
        }
      }
      this.$emit('leavelUp')
      this.log = 'OK'
      setTimeout(function() {
        self.log = undefined
      }, 1000)
      return
    },
    eventHook2: function() {
      let self = this
      let len = this.creditArr.length
      if (this.randomArr[len - 1] !== this.creditArr[len - 1]) {
        this.$emit('testErrStrict')
        this.log = 'ERR'
        setTimeout(function() {
          self.log = undefined
        }, 1000)
        return
      }
    }
  }
}

</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
.tester
  width 150px
  height 150px
  font-size 65px
  color #DC0D29
  line-height 150px
  text-align center
  background-color #363636
  border-radius 50%
  box-shadow 0px 1px 6px 0px rgba(0, 0, 0, 0.50)
  transition .5s
  user-select none
</style>
