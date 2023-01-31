<template>
  <view class="content" @touchstart="start" @touchend="end">
    <van-image class="logo" round fit="cover" src="/static/images/blue.png" />
    <van-form>
      <van-cell-group inset>
        <van-field v-model="name" name="姓名" label="姓名" placeholder="姓名">
          <template #left-icon>
            <van-icon
              class="iconfont"
              class-prefix="icon"
              color="#68A8E7"
              name="zujian-xingming"
            ></van-icon>
          </template>
        </van-field>
        <van-field v-model="age" name="年龄" label="年龄" placeholder="年龄">
          <template #left-icon>
            <van-icon
              class="iconfont"
              class-prefix="icon"
              color="#68A8E7"
              name="nianling"
            ></van-icon>
          </template>
        </van-field>
        <van-field v-model="phone" name="电话" label="电话" placeholder="电话">
          <template #left-icon>
            <van-icon
              class="iconfont"
              class-prefix="icon"
              color="#1C92D2"
              name="dianhua1"
            ></van-icon>
          </template>
        </van-field>
        <van-field v-model="email" name="邮箱" label="邮箱" placeholder="邮箱">
          <template #left-icon>
            <van-icon
              class="iconfont"
              class-prefix="icon"
              color="#1C92D2"
              name="youxiang"
            ></van-icon>
          </template>
        </van-field>
      </van-cell-group>
    </van-form>
  </view>
</template>

<script lang="ts">
import { onMounted, ref } from 'vue'

export default {
  setup() {
    onMounted(() => {})
    const name = ref('王鹏飞')
    const age = ref(26)
    const phone = ref('13888067018')
    const email = ref('Laofee@foxmail.com')
    return {
      name,
      age,
      phone,
      email,
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
      } else if (subX < -50) {
        console.log('右滑，下一页')
        uni.navigateTo({
          url: '../education/Education',
        })
      } else {
        console.log('无效')
      }
    },
  },
}
</script>

<style lang="scss">
body {
  background: linear-gradient(
    to bottom,
    rgb(127, 127, 213),
    rgb(134, 168, 231),
    rgb(145, 234, 228)
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 250rpx;
  width: 250rpx;
  margin-top: 180rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}
</style>
