<template>
  <div class="game-panel">
    <div class="blocks-wrapper">
      <slot name="blocks"></slot>
      <div class="tester-wrapper">
        <slot name="tester"></slot>
      </div>
    </div>
    <div class="operator-wrapper">
      <slot name="operator"></slot>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">

export default {
  data () {
    return {
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus" scoped>
.game-panel
  width 450px
  min-width 450px
  margin-top 70px
  background #fafafa
  border-radius 6px
  box-shadow 0px 1px 6px 0px rgba(0, 0, 0, 0.50)
  .blocks-wrapper
    position relative
    font-size 0
    div
      display inline-block
    .tester-wrapper
      position absolute
      left 50%
      top 50%
      margin-top -75px
      margin-left -75px
  .operator-wrapper
    position relative
    height 50px
    padding 10px 0
</style>
