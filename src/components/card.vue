<template>
  <div class='card' @click="openMusicList">
    <div :src="music.cover" class="image" :style="cover"/>
    <p class="version">vol.{{music.id}}</p>
    <h2 class="title">{{music.title}}</h2>
    <p class="create-date">#民谣 创建于 2018-07-12</p>
    <div><img class="play-btn" :src="image" @click="handleButtonClick"/></div>
  </div>
</template>

<script>

const playButton = require('../../static/assets/play-circle-fill.png')
const pauseButton = require('../../static/assets/poweroff-circle-fill.png')

export default {
  data () {
    return {
      image: playButton,
      isPsuse: true,
      cover: undefined
    }
  },
  props: {
    music: {
      required: true,
      type: Object
    }
  },
  methods: {
    handleButtonClick () {
      this.isPsuse = !this.isPsuse
      if (this.isPsuse) {
        this.image = playButton
      } else {
        this.image = pauseButton
      }
    },
    openMusicList () {
      const url = '../music-list/main'
      wx.navigateTo({ url })
    }
  },

  mounted () {
    console.info(this.music)
    this.cover = `background-image: url(${this.music.cover})` // :style = [object Object] Not Support
    console.info(this.cover)
  }
}
</script>

<style scoped>
.card {
  padding: 10px;
  flex: 1;
  border: 1px solid #f8f8f8;
  display: flex;
  width: 100%;
  box-shadow: 0 7px 21px rgba(56,56,56,.15);
  border-radius: 5px;
  flex-direction: column;
  overflow: hidden;
  align-items: center;
}

.version {
  width: 100%;
  margin: 10px 0 30px;
  text-align: center;
  color: #7d7d7d;
  font: 13px/22px Verdana,'微软雅黑','Microsoft YaHei',Helvetica,Arial;
}

.image {
  height: 200px;
  width: 100%;
  background-size: cover;
  border-radius: 3px;
  background-position: center;
}

.play-btn {
  width: 40px;
  height: 40px;
}

.create-date {
  font: 13px/22px Verdana,'微软雅黑','Microsoft YaHei',Helvetica,Arial;
  color: #7d7d7d;
  margin: 10px 0 40px;
}

</style>
