<!--Slider 组件-->
<!--
    props：
        width       -> 图片宽度 默认 100%  
        list        -> 数据列表 对象数组，格式 [{linkUrl:'url',picUrl:'url'}]
        loop        -> 是否循环轮播 默认 true
        autoPlay    -> 是否自动轮播 默认 true
        speed       -> 自动轮播速度 默认 3000
        dots        -> 是否显示 dots 默认 true
-->
<template> 
  <div class="slider" ref="slider">
      <div class="slider-group" ref="sliderGroup">
          <div class="slider-item" v-for="(item,index) in list" :key="index" >
              <a :href="item.linkUrl">
                  <img :src="item.picUrl" :alt="item.linkUrl" :style="`width:${width}`" ref="sliderItemImg">
              </a>
          </div>
      </div>
     <div class="dots" v-if="this.dots">
          <span :class="`dot ${index === currentPageIndex ? 'active' :'' }`" v-for="(item,index) in list.length" :key="index"></span>
      </div>
  </div>
</template>
<script>
import BScroll from "better-scroll";
export default {
  props: {
    // 图片宽度
    width: {
      type: String,
      default: "100%"
    },
    // 数据列表
    list: {
      type: Array,
      default: []
    },
    // 循环轮播
    loop: {
      type: Boolean,
      default: true
    },
    // 是否自动轮播
    autoPlay: {
      type: Boolean,
      default: true
    },
    // 轮播间隔
    speed: {
      type: Number,
      default: 3000
    },
    // 是否需要 dots
    dots: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      currentPageIndex: 0,
      _slider: null,
      _timer:null
    };
  },
  mounted() {
    const _this = this;
    _this.$nextTick(() => {
      _this._initSliderWidth();
      _this._initSlider();
      if(_this.autoPlay){
          _this._play();
      }
    });
  },
  methods: {
    /**
     * @name _initSliderWidth
     * @description 初始化slider容器Width
     * @author postbird
     */
    _initSliderWidth() {
      const imgWidth = this.$refs.sliderItemImg[0].clientWidth;
      let sliderWidth = imgWidth * this.list.length;
      if (this.loop) {
        // 循环轮播需要添加两个img DOM 的宽度
        sliderWidth += imgWidth * 2;
      }
      this.$refs.sliderGroup.style.width = sliderWidth + "px";
      this.$refs.sliderItemImg.forEach(item => {
        item.style.width = imgWidth + "px";
      });
    },
    /**
     * @name _initSlider
     * @description 初始化 better-scroll
     * @author postbird
     */
    _initSlider() {
        const _this = this;
        _this._slider = new BScroll(_this.$refs.slider, {
        scrollX: true,
        scrollY: false,
        momentum: false,
        click:true,
        snap: {
            loop: this.loop, // 循环
            threshold: 0.1
        }
        });
      // 获取当前页
      _this._getCurrentPageIndex();
      // 滚动之前 清除timer
      _this._slider.on('beforeScrollStart',()=>{
          clearInterval(_this._timer);
      });
    },
    /**
     * @name _getCurrentPageIndex
     * @description 获取当前的 pageIndex
     * @author postbird
     */
    _getCurrentPageIndex() {
        const _this = this;
        _this._slider.on("scrollEnd", () => {
        let index = _this._slider.getCurrentPage().pageX;
        _this.currentPageIndex = index;
        // 如果自动播放 则开启
        if(_this.autoPlay){
            _this._play();
        }
        });
    },
    /**
     * @name _play
     * @description 控制自动轮播
     * @author postbird
     */
    _play(){
        const _this =this;
        let pageIndex = _this.currentPageIndex;
        _this._timer = setInterval(() => {
            pageIndex++;
            if(pageIndex >= _this.list.length){
                pageIndex = 0;
            }
            _this._slider.goToPage(pageIndex);
        }, this.speed);
    },
  }
};
</script> 
<style scoped >
.slider {
  position: relative;
  min-height: 1px;
}
.slider .slider-group {
  position: relative;
  overflow: hidden;
  white-space: nowrap;
}
.slider .slider-group .slider-item {
  float: left;
  overflow: hidden;
  text-align: center;
}
.slider .slider-group .slider-item a {
  display: block;
  width: 100%;
  overflow: hidden;
  text-decoration: none;
}
.slider .slider-group .slider-item img {
  display: block;
  width: 100%;
}
.slider .dots {
  position: absolute;
  right: 0;
  left: 0;
  bottom: 12px;
  text-align: center;
  font-size: 0;
}
.slider .dot {
  display: inline-block;
  margin: 0 4px;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #dfdfdf;
}
.slider .dot.active {
  width: 20px;
  border-radius: 5px;
  background: #dfdfdf;
}
</style>
