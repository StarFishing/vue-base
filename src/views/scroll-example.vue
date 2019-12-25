<template>
  <div class="scroll-example">
    <Scroll :data="list"
            style="height:300px"
            :pull-down-refresh="true"
            @pullingDown="pullingDown"
            ref="scroll">

      <template #updateTop>
        <div class="update-top">
          更新成功1条数据
        </div>
      </template></Scroll>
  </div>
</template>

<script lang="ts">
import { Vue, Prop, Component } from 'vue-property-decorator'
// @ is an alias to /src
import Scroll from '@/components/scroll/scroll.vue'
@Component({
  components: {
    Scroll,
  },
})
export default class ScrollExample extends Vue {
  data = [
    '😁😁😁😁😁😁',
    '😅😅😅😅😅😅',
    '😋😋😋😋😋😋',
    '🧚‍♂️🧚‍♂️🧚‍♂️🧚‍♂️🧚‍♂️🧚‍♂️',
    '🧞‍♂️🧞‍♂️🧞‍♂️🧞‍♂️🧞‍♂️🧞‍♂️',
    '😡😡😡😡😡😡',
    '🧜‍♂️🧜‍♂️🧜‍♂️🧜‍♂️🧜‍♂️🧜‍♂️',
    '🧚‍♀️🧚‍♀️🧚‍♀️🧚‍♀️🧚‍♀️🧚‍♀️',
  ]
  list = ['😁😁😁😁😁😁']

  pullingDown() {
    setTimeout(() => {
      ;(this.$refs.scroll as any).isPullingDown = false
    }, 1000)

    setTimeout(() => {
      ;(this.$refs.scroll as any).finishPullDown()
      this.list.push(this.data[Math.floor(Math.random() * 8)])
    }, 1600)

    setTimeout(() => {
      let scroll = this.$refs.scroll as any
      scroll.beforePullDown = true
      scroll.refresh()
    }, 1800)
  }
}
</script>
<style lang="stylus" scoped>
.update-top
  background #07c160
  width 100vh
  height 30px
  text-align center
</style>
