<template>
  <div class="video-list">
    <swiper ref="mySwiper" :options="swiperOptions">
      <swiper-slide v-for="(item, index) in videoList" :key="index">
        <videos ref="videos" :video_url = "item.url" :index = "index"/>
        <video-info/>
        <right-bar/>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
import Videos from './Videos'
import VideoInfo from './VideoInfo'
import RightBar from './RightBar'
export default {
  name: 'VideoList',
  data() {
    return {
      index: 0,
      swiperOptions: {
        direction: 'vertical',
        grabCursor: true,
        setWrapperSize: true,
        autoHeight: true,
        slidesPerView: 1,
        mousewheel: true,
        mousewhellControl: true,
        height: window.innerHeight,
        resistanceRatio: 0,
        observeParents: true,
        on: {
          tap: () => {
            this.playAction(this.index)
          },
          slideNextTransitionStart: () => {
            this.index += 1
            this.nextVideo(this.index)
          },
          slidePrevTransitionEnd: () => {
            if (this.index > 0) {
              this.index -= 1
              this.preVideo(this.index)
            }
          }
        }
      },
      videoList: [
        {
          id: '1',
          url: 'https://cdn.jsdelivr.net/gh/honjun/hojun@1.2/Unbroken.mp4'
        },
        {
          id: '2',
          url: 'https://cdn.jsdelivr.net/gh/kali65536/cdnmovie@master/mv/kali-%E4%BD%95%E5%BF%85%E5%9C%A8%E4%B9%8E%E6%88%91%E6%98%AF%E8%B0%81cover%E6%9D%8E%E5%AE%97%E7%9B%9B(%E8%B6%85%E6%B8%85).mp4'
        },
        {
          id: '3',
          url: 'https://cdn.jsdelivr.net/gh/honjun/hojun@1.2/Unbroken.mp4'
        },
        {
          id: '4',
          url: 'https://cdn.jsdelivr.net/gh/kali65536/cdnmovie@master/mv/kali.mp4'
        }
      ]
    }
  },
  methods: {
    playAction() {
      this.$refs.videos[this.index].playOrStop()
    },

    // 下一个视频
    nextVideo() {
      this.$refs.videos[this.index - 1].stop()
      this.$refs.videos[this.index].play()
    },

    // 上一个视频
    preVideo() {
      this.$refs.videos[this.index + 1].stop()
      this.$refs.videos[this.index].play()
    }
  },
  components: {
    RightBar,
    Swiper,
    SwiperSlide,
    Videos,
    VideoInfo
  }
}
</script>

<style scoped>
.video-list .swiper-container{
  height: 100%;
  position: relative;
}
</style>
