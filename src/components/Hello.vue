<template>
  <div class="page-loadmore">
    <div class="page-loadmore-wrapper" ref="wrapper" :style="{ height: wrapperHeight + 'px' }">
      <mt-loadmore :top-method="loadTop" @top-status-change="handleTopChange"       :bottom-method="loadBottom" 
      @bottom-status-change="handleBottomChange" :bottom-all-loaded="allLoaded" ref="loadmore">      
        
        
        <div style="width:100%;height:900px;background:#003150;"></div>
      
      
      
      
      
      
       <div slot="top" class="mint-loadmore-top">
          <div v-show="topStatus !== 'loading'" >
              <span v-if="topStatus === 'drop'">释放刷新</span>
              <span v-else>下滑</span>
              <span :class="{ 'is-rotate': topStatus === 'drop' }">↓</span>         
          </div>       
          <span v-show="topStatus === 'loading'">
            <mt-spinner type="snake"></mt-spinner>
          </span>
        </div>    
        <div slot="bottom" class="mint-loadmore-bottom">     
          <div v-show="bottomStatus !== 'loading'">
             <span :class="{ 'is-rotate': bottomStatus === 'drop' }">↑</span>
             <span v-if="bottomStatus === 'drop'">释放加载</span>
             <span v-else>上滑</span>
          </div>
          <span v-show="bottomStatus === 'loading'">
            <mt-spinner type="snake"></mt-spinner>
          </span>
        </div>
      </mt-loadmore>
    </div>
  </div>
</template>
<style>
.loading-background, .mint-loadmore-top span {
    -webkit-transition: .2s linear;
    transition: .2s linear
}
.mint-loadmore-top span {
    display: inline-block;
    vertical-align: middle
}
.mint-loadmore-top span.is-rotate {
    -webkit-transform: rotate(180deg);
    transform: rotate(180deg)
}
.page-loadmore .mint-spinner {
    display: inline-block;
    vertical-align: middle
}
.page-loadmore-wrapper {
    overflow: scroll
}
.mint-loadmore-bottom span {
    display: inline-block;
    -webkit-transition: .2s linear;
    transition: .2s linear;
    vertical-align: middle
}
.mint-loadmore-bottom span.is-rotate {
    -webkit-transform: rotate(180deg);
    transform: rotate(180deg)
}
</style>
<script type="text/babel">
  export default {
    data() {
      return {
        allLoaded: false,
        bottomStatus: '',
        wrapperHeight: 0,
        topStatus: ''
      };
    },
    methods: {
      handleBottomChange(status) {
        this.bottomStatus = status;
      },
      loadBottom() {
        setTimeout(() => {
          this.$refs.loadmore.onBottomLoaded();
        }, 1500);
      },
      handleTopChange(status) {
        this.topStatus = status;
      },
      loadTop() {
        setTimeout(() => {
          this.$refs.loadmore.onTopLoaded();
        }, 1500);
      }
   
},
 mounted() {
      this.wrapperHeight = document.documentElement.clientHeight - this.$refs.wrapper.getBoundingClientRect().top;
    }
  };
</script>