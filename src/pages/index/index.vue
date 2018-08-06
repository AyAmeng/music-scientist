<template>
  <div class="index-page" @click="clickHandle('test click', $event)">

      <div class="userinfo" @click="bindViewTap">
        <img class="app-index" v-if="userInfo.avatarUrl" :src="imageUrl" background-size="cover" />
        <h2 class="title">醉心民谣</h2>
      </div>

      <div class="usermotto">
        <div class="user-motto">

          <p>跳进这汹涌的人潮里吧</p>

          <p>带着少年慌乱的舞步</p>

          <p>带着藏匿在心底的不合时宜</p>

          <p>没有人能够带走夏天</p>

          <p>因为夏天永不会结束</p>

          <p>让你从新聆听这个夏天</p>

        </div>
      </div>
      <!-- <Card :header="{title: '2'}"/> -->
      <!-- <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a> -->
  </div>
</template>

<script>
const imageUrl = require('../../../static/assets/index.jpeg')

export default {
  data () {
    return {
      motto: 'Hello Music',
      userInfo: {},
      imageUrl: imageUrl
    }
  },

  components: {
  },

  mounted () {
    // this.timer = setTimeout(() => {
    //   console.info('mounted')
    //   console.info(window, clearTimeout)
    //   wx.navigateTo({ url: '../HomePage/main' })
    // }, 3000)
  },
  beforeDestroy () {
    console.info('window')

    if (this.timer) {
      console.info(window)
      clearTimeout(this.timer)
    }
  },

  destroyed () {
    console.info('window')
  },

  methods: {
    bindViewTap () {
      const url = '../HomePage/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              console.info(res)
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.title {
  margin-top: 20px;
}

.app-index {
  width: 100%;
  height: 200px;
  border-radius: 5px;
}

.index-page {
  margin: 20px;
}

.userinfo-nickname {
  color: #aaa;
}

.user-motto p {
  margin-top: 10px;
  text-align: center;
}

.usermotto {
  margin-top: 60px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
