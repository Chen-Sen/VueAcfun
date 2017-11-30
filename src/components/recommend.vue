<template>
  <div class="wrap">
    <!-- 轮播图 -->
    <a-swipe :recommend="this.recommend"></a-swipe>
    <div class="content-wrap">
      <ul>
        <li class="content-item" v-for="(item,index) in arr.vdata">
          <div class="content-video" v-if="item.type.value!=='banners'">
            <div class="monkey-topLine">
              <img :src="item.image" alt="" class="fl">
              <h4>{{item.name}}</h4>
            </div>
            <div class="top-content">
              <div class="top-item col-xs-6" @click='recommendPlay(item.id,item.title, item.intro, item.author)'
                   v-for="item in item.contents" key="item.aid">
                <img :src="item.image" alt="" class="show-img">
                <div class="top-info">
                  <span class="top-title">{{item.title}}</span>
                </div>
              </div>
            </div>
            <div class="content-banner">
              <p>查看更多</p>
            </div>
          </div>

        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  import aSwipe from '@/components/swipe.vue'
  export default {
    data() {
      return {
        recommend: [],
        arr: [],
      }
    },
    components: {
      aSwipe
    },
    computed: {
      recommendList() {
        return this.$store.state.recommendList;
      }
    },
    created() {
      let self = this
      this.$axios.get('api/recommend')
        .then((response) => {
          response = response.data
          if (response.error === 0) {
            self.recommend = response.data.vdata[0].contents
            self.arr = response.data
            self.arr.vdata.shift()
            self.$store.state.recommendList = self.recommend.vdata;
          }
        })
        .catch((error) => {
          alert(error)
        })
    },
    methods: {
      recommendPlay(aid, title, description, author) {
        this.$router.push({
          name: 'recommendPlay',
          params: {
            'aid': aid
          }
        })
        this.$store.state.recommendTitle = title
        this.$store.state.recommendDesc = description
        this.$store.state.recommendAuthor = author
      }
    }
  }
</script>

<style lang="less" scoped>
  @import '../assets/css/recommend.less';
</style>
