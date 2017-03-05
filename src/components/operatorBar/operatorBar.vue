<template>
  <div class="operator-bar">
		<transition-group name="fade" mode="in-out">
	    <div v-show="!gaming" :key="'1'">
	    	<i class="fa fa-play" @click="startGame">&nbsp;Start</i>
	    	<i class="fa" :class="{ 'fa-toggle-on': strictMode, 'fa-toggle-off': !strictMode }"  @click="strictModeToggle">&nbsp;Strict Mode</i>
	    </div>
	    <div v-show="gaming" :key="'2'">
	    	<i class="fa fa-stop" @click="exitGame">&nbsp;Stop</i>
	    	<i class="fa fa-repeat" @click="repeatGame">&nbsp;Repeat</i>
	    	<i class="fa" :class="{ 'fa-toggle-on': strictMode, 'fa-toggle-off': !strictMode }"  @click="strictModeToggle">&nbsp;Strict Mode</i>
	    </div>
    </transition-group>
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
.operator-bar
  font-size 0
  div
  	position absolute
  	width 100%
  i.fa
  	display inline-block
  	margin 10px
  	font-size 26px
  	color #909090
  	transition color .5s
		user-select none
	i.fa:hover
		color #007fff
.fade-enter-active, .fade-leave-active
  transition opacity .5s
.fade-enter, .fade-leave-active
  opacity 0
// .fade-enter
//   opacity 0
//   transform translateX(-100%)
// .fade-enter-active, .fade-leave-active 
//   transition all 0.65s
// .fade-leave-active 
//   opacity 0
//   transform translateX(100%)
</style>
