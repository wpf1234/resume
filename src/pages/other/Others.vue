<template>
  <view class="content" @touchstart="start" @touchend="end">
    <h1>此页两个内容： 1.2021~2022 考研 2.个人作品</h1>
  </view>
</template>

<script lang="ts">
import {
  reactive,
  toRefs,
  onBeforeMount,
  onMounted,
  getCurrentInstance,
} from 'vue'
export default {
  name: 'Others',
  props: [],
  setup() {
    const ctx = getCurrentInstance()
    console.log(ctx)
    console.log('1-开始创建组件-setup')
    const data = reactive({})
    onBeforeMount(() => {
      console.log('2.组件挂载页面之前执行----onBeforeMount')
    })
    onMounted(() => {
      console.log('3.-组件挂载到页面之后执行-------onMounted')
    })
    const refData = toRefs(data)
    return {
      ...refData,
    }
  },
  data() {
    return {
      startData: {
        clientX: 0,
        clientY: 0,
      },
    }
  },
  methods: {
    start(e) {
      // console.log('开始下滑坐标', e.changedTouches[0].clientY)
      this.startData.clientX = e.changedTouches[0].clientX
      this.startData.clientY = e.changedTouches[0].clientY
    },
    end(e) {
      // console.log('结束下滑坐标', e.changedTouches[0].clientY)
      const subX = e.changedTouches[0].clientX - this.startData.clientX
      const subY = e.changedTouches[0].clientY - this.startData.clientY
      if (subY < -50) {
        // console.log('下滑')
      } else if (subY > 50) {
        console.log('上滑')
      } else if (subX > 50) {
        console.log('左滑，返回上一页')
        uni.navigateTo({
          url: '../workExp/Work',
        })
      } else if (subX < -50) {
        console.log('右滑，下一页')
      } else {
        console.log('无效')
      }
    },
  },
}
</script>
<style lang="scss" scoped></style>
