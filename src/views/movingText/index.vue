<template>
  <div class="box">
    <div ref="text" class="text">
      {{ text }}
      <!-- auto scroll text auto scroll textauto scroll textauto scroll textauto
      scroll text -->
    </div>
  </div>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      default: 'auto scroll text auto scroll textauto scroll text'
    }
  },
  mounted() {
    this.scrollJedge()
  },
  methods: {
    loop(width, scrollWidth, clientWidth, dom) {
      setTimeout(() => {
        if (width - 0.5 > 0) {
          console.log(55, (width -= 0.5), `translateX(-${(width -= 0.5)}px)`)
          dom.style.transform = `translateX(-${(width -= 0.5)}px)`
          this.loop(width, scrollWidth, clientWidth, dom)
        } else {
          setTimeout(() => {
            width = scrollWidth - clientWidth
            dom.style.transform = `translateX(0px)`
            this.loop(width, scrollWidth, clientWidth, dom)
          }, 1000)
        }
      }, 30)
    },
    scrollJedge() {
      // 获取dom
      const dom = this.$refs.text
      const scrollWidth = dom.scrollWidth
      const clientWidth = dom.clientWidth
      const width = scrollWidth - clientWidth
      // 执行动画
      this.loop(width, scrollWidth, clientWidth, dom)
    }
  }
}
</script>

<style scoped>
.box {
  width: 100px;
  /* 给第三方使用时，这里设置为100% */
  overflow: hidden;
}
.text {
  /* 文字隐藏后添加省略号 */
  /* text-overflow: ellipsis; */
  /* 强制不换行 */
  white-space: nowrap;
}
</style>
