<template>
  <div class="fullpage-container">
    <div class="fullpage-container-fill">
      <div class="scroll-fullpage" :style="{ top: top }" ref="fullpage">
        <div
          id="hook1"
          class="section section01"
          :class="{ active: scrollindex === 0 }"
          @touchstart="scrollTouchStart"
          @touchmove="scrollTouchMove"
          @touchend="scrollTouchEnd"
        >
          <div class="cont">
            <div class="cont-body">
              <h1>排队挂号</h1>
              <h3>腰腿痛--->建议前往骨伤科就诊</h3>
              <p>①</p>
              <h4>↓↓↓↓↓</h4>
            </div>
          </div>
        </div>

        <div
          id="hook2"
          class="section section02"
          :class="{ active: scrollindex === 1 }"
          @touchstart="scrollTouchStart"
          @touchmove="scrollTouchMove"
          @touchend="scrollTouchEnd"
        >
          <div class="cont">
            <div class="cont-body">
              <h1>前往骨伤科</h1>
              <h3>三楼，电梯口右侧</h3>
              <p>②</p>
              <h4>↓↓↓↓↓</h4>
            </div>
          </div>
        </div>

        <div
          id="hook3"
          class="section section03"
          :class="{ active: scrollindex === 2 }"
          @touchstart="scrollTouchStart"
          @touchmove="scrollTouchMove"
          @touchend="scrollTouchEnd"
        >
          <div class="cont">
            <div class="cont-body">
              <h1>预约医师</h1>
              <h3>请将您的挂号单与前台处扫描</h3>
              <p>③</p>
              <h4>↓↓↓↓↓</h4>
            </div>
          </div>
        </div>

        <div
          id="hook4"
          class="section section04"
          :class="{ active: scrollindex === 3 }"
          @touchstart="scrollTouchStart"
          @touchmove="scrollTouchMove"
          @touchend="scrollTouchEnd"
        >
          <div class="cont">
            <div class="cont-body">
              <h1>收费处缴纳医药费</h1>
              <h3>一楼，大厅，进大门右手处</h3>
              <p>④</p>
              <h4>↓↓↓↓↓</h4>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      scrollindex: 0, // 当前页面的索引值
      totalPageNum: 4, // 总共页面数
      starty: 0, // 开始的位置x
      startTime: 0, // 开始的时间戳
      endy: 0, // 结束的位置y
      endTime: 0, // 结束的时间戳
      critical: 120, // 触发翻页的临界值
      maxTimeCritical: 300, // 滑动的时间戳临界值上限
      minTimeCritical: 100 // 滑动的时间戳临界值下限
    };
  },
  computed: {
    top() {
      // 计算当前往上的距离
      return this.scrollindex * -100 + 'vh';
    }
  },
  methods: {
    scrollTouchStart(e) {
      e = e.mp;
      // 获取开始点击点
      this.starty = e.touches[0].pageY;
      // 获取当前点击时间
      this.startTime = e.timeStamp;
    },
    scrollTouchMove(e) {},
    scrollTouchEnd(e) {
      e = e.mp;
      // 获取结束位置
      this.endy = e.changedTouches[0].pageY;
      // 间隔时间
      this.endTime = e.timeStamp;
      let timeStampdiffer = this.endTime - this.startTime;

      if (
        // 此时判断是滑动的时间差
        timeStampdiffer <= this.maxTimeCritical &&
        timeStampdiffer > this.minTimeCritical &&
        // 此时判断已经改变了 初始位置 > 当前位置
        this.starty > e.changedTouches[0].pageY
      ) {
        // 手势上滑  移动
        this.scrollindex =
          this.scrollindex >= this.totalPageNum-1 ? this.scrollindex : this.scrollindex + 1;
      } else if (
        // 判断时间
        timeStampdiffer <= this.maxTimeCritical &&
        timeStampdiffer > this.minTimeCritical &&
        // 初始位置 < 当前位置  手势下滑
        this.starty < e.changedTouches[0].pageY
      ) {
        // 手势下滑 移动
        this.scrollindex = this.scrollindex <= 0 ? 0 : this.scrollindex - 1 ;
      }
    }
  }
};
</script>

<style lang="wxss">
#hook1 {
  background: #9999cc;
}
#hook2 {
  background: #cc66cc;
}
#hook3 {
  background: #cc99cc;
}
#hook4 {
  background: #cccccc;
}

.cont{
  position: relative;
}
.cont-body h4{
  position: absolute;
  bottom: 100rpx;
  font-size: 48rpx;
  left: 45%;
  color: #fff;
}
.cont-body p{
  text-align: center;
  font-size: 80rpx;
  color: #fff;
  margin-top: 300rpx;
}

page {
  height: 100%;
  background: #fff;
  color: #282828;
}
.fullpage-container {
  height: 100%;
  flex: 1;
  flex-direction: column;
  box-sizing: border-box;
  padding: 0;
  align-items: initial;
  justify-content: first baseline;
}
.fullpage-container-fill {
  height: 100%;
  overflow: hidden;
  position: relative;
}
.scroll-fullpage {
  box-sizing: border-box;
  position: absolute;
  /* 增加动画*/
  transition: top .3s linear;
}

.section {
  width: 100vw;
  height: 100vh;
  position: relative;
}
.cont {
  width: 100%;
  height: 100%;
  margin: 0 auto;
}

</style>
