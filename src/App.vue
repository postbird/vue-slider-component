<template>
  <div id="app">
      <p class="title">演示图片来自：https://y.qq.com/</p>
      <p class="title">建议在移动端进行查看</p>
      <app-slider :list="sliders" :loop="true" v-if="sliders.length" width="100%" ></app-slider>
   </div>
</template>

<script>
import Slider from './components/Slider';
export default {
  name: 'app',
  data () {
    return {
      sliders:[
        {
          linkUrl:'http://y.qq.com/w/album.html?albummid=001RsOK33No4Sz&ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:'https://y.gtimg.cn/music/photo_new/T003R720x288M000001EwfWs4QSIl6.jpg?max_age=2592000'
        },
        {
          linkUrl:'https://y.qq.com/msa/270/0_5102.html?ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:'https://y.gtimg.cn/music/photo_new/T003R720x288M000001CV9tc1xK59w.jpg?max_age=2592000'
        },
        {
          linkUrl:'https://y.qq.com/m/client/music_headline/index.html?_hidehd=1&_button=2&zid=689728&ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:'https://y.gtimg.cn/music/photo_new/T003R720x288M000002n0L9H3Bf8F0.jpg?max_age=2592000'
        },
        {
          linkUrl:'http://y.qq.com/w/album.html?albummid=001cTmxl1t64WK&ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:'https://y.gtimg.cn/music/photo_new/T003R720x288M000001pf9Sy13Evav.jpg?max_age=2592000'
        },
        {
          linkUrl:'https://y.qq.com/msa/324/0_5116.html?ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:'https://y.gtimg.cn/music/photo_new/T003R720x288M000002QkMgs2GfWgL.jpg?max_age=2592000'
        },
      ]
    }
  },
  components:{
    'app-slider':Slider
  }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing: border-box;
}
@media screen and (min-width:769px){
  html,body{
    max-width: 720px;
    overflow: hidden;
    margin:0 auto;
  }
}
.title{
  margin:10px 0;
}
</style>
