<template>
  <div class="wrap">
    <div class="disport-header">
      <a-swipe></a-swipe>
      <ul class="disport-nav">
        <li v-for="item in disport.vdata[0].contents">{{item.title}}</li>
      </ul>
    </div>
    <div class="hot-disport">
      <ul class="content-wrap">
        <li class="content-item" v-for="item in disport.vdata" v-if="item.type.value !=='channels'&&item.type.value !=='banners'">
          <img :src="item.image" alt="" class="fl">
          <h4>{{item.name}}<span style="float: right;margin-right: 10px; color: #FA7198">更多>></span></h4>
          <div class="disport-content">
            <div class="disport-item col-xs-6 fl" v-for="item in item.contents"
                 @click='disportPlay(item.url,item.title, item.author)'>
              <img :src="item.image" alt="" class="disport-img">
              <div class="disport-info">
                <span class="disport-title">{{item.title}}</span>
              </div>
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
        disport: []
      }
    },
    components: {
      aSwipe
    },
    computed: {
      disportList() {
        return this.$store.state.disportList;
      }
    },
    created() {
      let self = this
      this.$axios.get('api/disport')
        .then((response) => {
          response = response.data
          if (response.error === 0) {
            self.disport = response.data
            console.log(self.disport)
          }
        })
        .catch((error) => {
          alert(error)
        })
    },
    methods: {
      disportPlay(aid, title, author) {
        this.$router.push({
          name: 'disportPlay',
          params: {
            'aid': aid
          }
        })
        this.$store.state.disportTitle = title
        this.$store.state.disportAuthor = author
      }
    }
  }
</script>

<style lang="less" scoped>
  @import '../assets/css/disport.less';
</style>
