<template>
  <div class="wrap">
    <img src="../assets/img/drama-banner.png" alt="" class="drama-banner">
    <ul class="drama-nav">
      <li v-for="item in titleArr.vdata[1].contents">{{item.title}}</li>
    </ul>
    <div class="new-drama">
      <ul>
        <li v-for="(item,index) in titleArr.vdata" v-if="item.type.value !=='channels'&&item.type.value !=='banners'">
          <img :src="item.image" alt="" class="fl">
          <h4>{{item.name}}<span style="float: right;margin-right: 10px; color: #FA7198">更多>></span></h4>
          <div class="drama-content">
            <div class="drama-item col-xs-4 fl" @click="dramaPlay(item.id,item.title,item.intro)" v-for="item in item.contents">
              <img :src="item.image" alt="" class="drama-img">
              <div class="drama-info">
                <span class="drama-title">{{item.title}}</span>
                <p class="drama-num" v-if="item.latestBangumiVideo">更新至{{item["latestBangumiVideo"].title}}</p>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        animation: [],
        titleArr: []
      }
    },
    computed: {
      dramaList() {
        return this.$store.state.dramaList;
      }
    },
    created() {
      let self = this
      this.$axios.get('api/animation')
        .then((response) => {
          response = response.data
          if (response.error === 0) {
            self.titleArr = response.data
//            this.animationFn()
          }
        })
        .catch((error) => {
          alert(error)
        })
    },
    methods: {
      dramaPlay(season_id, title,intro) {
        this.$router.push(
          {name: 'dramaPlay', params: {'season_id': season_id}}
        )
        this.$store.state.dramaTitle = title
        this.$store.state.disportDesc = intro
      },
      latestBangumiVideoFn(item){
          console.log(item)
      }
    }

  }
</script>

<style lang="less" scoped>
  @import '../assets/css/drama.less';
</style>
