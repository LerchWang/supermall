<template>
  <div class="goodlist">
    <good-list-item v-for="(item, index) in goods" :key="index" :goodItem="item" class="item"></good-list-item>
  </div>
</template>

<script>
import GoodListItem from './GoodListItem'

export default {
  name: 'GoodList',
  data() { 
    return {

    }
  },
  props: {
    goods: {
      type: Array,
      default: function(){
        return []
      }
    }
  },
  components:{
    GoodListItem
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
.goodlist {
  display: flex;
  flex-wrap: wrap;
  padding: 5px;
  justify-content: space-around;
}
.goodlist .item {
  width: 48%;
}

</style>