<template>
  <div class="operator-bar-wrapper">
    <div class="operator-bar">
      <transition-group name="fade">
        <div v-show="!gaming" class="operator-team" :key="'operator-team1'">
          <i class="fa fa-play" @click="startGame">&nbsp;Start</i>
          <i class="fa" :class="{ 'fa-toggle-on': strictMode, 'fa-toggle-off': !strictMode }"  @click="strictModeToggle">&nbsp;Strict Mode</i>
        </div>
        <div v-show="gaming" class="operator-team" :key="'operator-team2'">
          <i class="fa fa-stop" @click="exitGame">&nbsp;Stop</i>
          <i class="fa fa-repeat" @click="repeatGame">&nbsp;Repeat</i>
          <i class="fa" :class="{ 'fa-toggle-on': strictMode, 'fa-toggle-off': !strictMode }"  @click="strictModeToggle">&nbsp;Strict Mode</i>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  data() {
    return {
      gaming: false,
      strictMode: false
    }
  },
  methods: {
    startGame() {
      this.$emit('startGame')
      this.gaming = true
    },
    exitGame() {
      this.$emit('exitGame')
      this.gaming = false
    },
    repeatGame() {
      this.$emit('repeatGame')
    },
    strictModeToggle() {
      this.strictMode = !this.strictMode
      this.$emit('strictModeChange', this.strictMode)
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
.operator-bar-wrapper
  height 45px
  .operator-bar
    font-size 0
    clear both
    text-align center
    .operator-team
      position absolute
      width 100%
      left 0
      .fa
        display inline-block
        margin 10px
        font-size 26px
        color #909090
        transition color .5s
        user-select none
        &:hover
          color #007fff
.fade-enter
  opacity 0
  transform translate3d(0, -30%, 0)
.fade-enter-active, .fade-leave-active 
  transition all 0.65s
.fade-leave-active 
  opacity 0
  transform translate3d(0, 30%, 0)
</style>
