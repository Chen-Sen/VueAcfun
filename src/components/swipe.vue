<template>
  <div class="wrap">
    <div class="swipe">
      <mt-swipe :auto="2000">
        <mt-swipe-item>
          <img :src="this.item[0].image">
        </mt-swipe-item>
        <mt-swipe-item>
          <img :src="this.item[1].image">
        </mt-swipe-item>
        <mt-swipe-item>
          <img :src="this.item[2].image">
        </mt-swipe-item>
        <mt-swipe-item>
          <img :src="this.item[3].image">
        </mt-swipe-item>
        <mt-swipe-item>
          <img :src="this.item[4].image">
        </mt-swipe-item>
      </mt-swipe>
    </div>
  </div>
</template>

<script>
  import {Swipe, SwipeItem} from 'mint-ui';
  export default {
    props: {
      recommend: {
        type: Array
      }
    },
    data() {
      return {
        item: []
      }
    },
    computed: {
//        banner () {
//          return this.$store.state.banner
//        }
    },
    watch: {
      recommend(val){
        if (val) {
          this.$nextTick(() => {
            this.item = val
          })
        }
      }
    }

    // 生命周期钩子函数，在created函数中调用ajax获取页面初始化所需的数据。
//      created () {
//          this.axios.get('/api/banner')
//            .then(res => {
//              this.$store.state.banner=res.data.data
////              console.log(res)
//            })
//      }
  }
</script>

<style lang="less" scoped>
  @import '../assets/css/swipe.less';
</style>
