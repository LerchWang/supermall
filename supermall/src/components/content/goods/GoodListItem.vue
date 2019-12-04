<template>
  <div class="goodlist-item">
    <img :src="goodItem.show.img" alt="">
    <div class="item-info">
      <p>{{goodItem.title}}</p>
      <span class="price">{{goodItem.price}}</span>
      <span class="collect">{{goodItem.cfav}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GoodListItem',
  data() { 
    return {

    }
  },
  props: {
    goodItem: {
      type: Object,
      default: function(){
        return {}
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
  .goodlist-item {
    padding-bottom: 40px;
    position: relative;
  }
  .goodlist-item img {
    width: 100%;
    border-radius: 5px;
  }
  .item-info {
    font-size: 12px;
    position: absolute;
    bottom: 5px;
    left: 0;
    right: 0;
    overflow: hidden;
    text-align: center;
  }
  .item-info p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    margin-bottom: 3px;
  }
  .item-info .price {
    color: var(--color-high-text);
    margin-right: 20px;
  }
  .item-info .collect {
    position: relative;
  }
  .item-info .collect::before {
    content: '';
    position: absolute;
    left: -15px;
    top: -1px;
    width: 14px;
    height: 14px;
    background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
  }
</style>