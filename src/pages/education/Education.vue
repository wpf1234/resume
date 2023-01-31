<template>
  <view class="content" @touchstart="start" @touchend="end">
    <van-card>
      <template #title>
        <h2>海南大学</h2>
      </template>
      <template #thumb>
        <van-image
          class="logo"
          fit="fill"
          src="../../static/images/HNLogo.png"
        />
      </template>

      <template #tags>
        <van-tag plain type="primary">211</van-tag>
        <van-tag class="tag" plain type="primary">双一流</van-tag>
      </template>
      <template #footer>
        <van-field
          v-model="year"
          name="学年"
          label="学年"
          placeholder="学年学制"
        />
        <van-field
          v-model="degree"
          name="学位"
          label="学位"
          placeholder="学位"
        />
        <van-field
          v-model="major"
          name="专业"
          label="专业"
          placeholder="专业"
        />
      </template>
    </van-card>
  </view>

  <view class="credential">
    <van-image
      class="graduate"
      fit="cover"
      src="../../static/images/graduate.jpg"
    />
    <van-image
      class="degree"
      fit="cover"
      src="../../static/images/degree.jpg"
    />
  </view>
</template>

<script lang="ts">
import { onBeforeMount, onMounted, ref } from 'vue'
export default {
  name: 'Educatuion',
  setup() {
    onBeforeMount(() => {})
    onMounted(() => {})
    const year = ref('4年')
    const major = ref('计算机科学与技术')
    const degree = ref('学士学位')
    return {
      year,
      major,
      degree,
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
          url: '../index/index',
        })
      } else if (subX < -50) {
        console.log('右滑，下一页')
        uni.navigateTo({
          url: '../workExp/Work',
        })
      } else {
        console.log('无效')
      }
    },
  },
}
</script>
<style lang="scss" scoped>
body {
  background: #e2e2e2;
}

.content {
  width: 100%;
  position: absolute;
  margin-top: 200rpx;
  align-items: center;
}
.logo {
  width: 200rpx;
  height: 200rpx;
  transform: scale(0.72);
}
.tag {
  left: 10rpx;
}
.credential {
  position: fixed;
  top: 750rpx;
}
.graduate {
  width: 320rpx;
  height: 320rpx;
  left: 40rpx;
}

.degree {
  width: 320rpx;
  height: 320rpx;
  left: 60rpx;
}
</style>
