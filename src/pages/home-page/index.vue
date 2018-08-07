<template>
  <div class="container">
    <Card :music="music"/>
  </div>

</template>

<script>
import Card from '@/components/card'
const music = require('../../utils/music.json')
const imageUrl = require('../../../static/assets/1.jpeg')

export default {
  data () {
    return {
      motto: 'Hello Music',
      userInfo: {},
      imageUrl: imageUrl,
      music: music[0]
    }
  },

  components: {
    Card
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
  .container {
    height: 100vh;
    padding: 40px 40px 100px;
  }
</style>
