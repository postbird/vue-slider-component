<template>
  <div id="app">
      <p class="title">演示图片来自：https://y.qq.com/ （侵权联系删除）</p>
      <p class="title">建议在移动端进行查看</p>
      <p class="title">如果图片第一次未加载，则刷新页面即可</p>
      <app-slider :list="sliders" :loop="true" v-if="sliders.length" width="100%" ></app-slider>
   </div>
</template>
 
<script>
import Slider from './components/Slider';
import pic1 from './assets/images/1.jpg';
import pic2 from './assets/images/2.jpg';
import pic3 from './assets/images/3.jpg';
import pic4 from './assets/images/4.jpg';
import pic5 from './assets/images/5.jpg';
export default {
  name: 'app',
  data () {
    return {
      sliders:[
        {
          linkUrl:'http://y.qq.com/w/album.html?albummid=001RsOK33No4Sz&ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:pic1
        },
        {
          linkUrl:'https://y.qq.com/msa/270/0_5102.html?ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:pic2
        },
        {
          linkUrl:'https://y.qq.com/m/client/music_headline/index.html?_hidehd=1&_button=2&zid=689728&ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:pic3
        },
        {
          linkUrl:'http://y.qq.com/w/album.html?albummid=001cTmxl1t64WK&ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:pic4
        },
        {
          linkUrl:'https://y.qq.com/msa/324/0_5116.html?ADTAG=myqq&from=myqq&channel=10007100',
          picUrl:pic5
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
