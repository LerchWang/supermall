<template>
  <div class="recommend">
    <div class="recommend-item" v-for="(item, index) in recommends" :key="index">
      <a :href="item.link">
        <img :src="item.image" alt="">
        <p>{{item.title}}</p>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecommendView',
  data() { 
    return {

    }
  },
  props: {
    recommends: {
      type: Array,
      default: function(){
        return []
      }
    }
  },
  components:{
  },
  mounted() {

  },
  methods:{

  },
  beforeCreate() {}, //生命周期 - 创建之前
  beforeMount() {}, //生命周期 - 挂载之前
  beforeUpdate() {}, //生命周期 - 更新之前
  updated() {}, //生命周期 - 更新之后
  beforeDestroy() {}, //生命周期 - 销毁之前
  destroyed() {}, //生命周期 - 销毁完成
  activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
 }
</script>

<style scoped>
.recommend {
  display: flex;
  font-size: 14px;
  margin-top: 10px;
  padding-bottom: 30px;
  border-bottom: 10px solid #eee;
}
.recommend-item {
  flex: 1;
  text-align: center;
}
.recommend img {
  width: 75px;
  height: 75px;
  margin-bottom: 10px;
}
</style>