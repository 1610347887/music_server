<template>
  <div class="song-audio">
    <audio id="player"
           :src="url"
           controls="controls"
           preload="auto"
           @canplay="startPlay"
           @ended="ended">

    </audio>
  </div>
</template>

<script>
import {mapGetters} from 'vuex'
export default {
  name: 'song-audio',
  computed:{
    ...mapGetters([
      'id',
      'url',
      'isPlay'
    ])
  },
  watch:{
    // 监听播放还是暂停状态
    isPlay: function (){
      this.togglePlay();
    }
  },
  methods:{
    // 获取链接后播放
    startPlay(){
      let player = document.querySelector('#player');
      // 开始播放
      player.play();
    },
    // 播放结束后触发
    ended(){
      this.isPlay = false
    },
    // 开始、暂停
    togglePlay(){
      let player = document.querySelector('#player');
      if (this.isPlay){
        player.play()
      }else {
        player.pause()
      }
    }
  }
}
</script>

<style>
  .song-audio{
    /*不显示播放器*/
    display: none;
  }
</style>
