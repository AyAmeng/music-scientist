<template>
  <div class="music-list">
    <img :src="music.cover"/>
    列表详情
  </div>

</template>

<script>
const music = require('../../utils/music.json')

export default {
  data () {
    return {
      music: music[0]
    }
  },

  mounted () {
    setTimeout(() => {
      console.info('mounted')
    })
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
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
  .music-list {
    height: 100vh;
    padding: 10px;
  }

  img {
    width: 100%;
    height: 200px;
    border-radius: 5px;
  }
</style>
