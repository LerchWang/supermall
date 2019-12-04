<template>
  <div class="tab-control">
    <div class="tab-control-item" 
         v-for="(item, index) in titles" :key="index"
         @click="itemClick(index)"
         :class="{active: index === currentIndex}">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TabControl',
  data() { 
    return {
      currentIndex:0
    }
  },
  props: {
    titles: {
      type: Array,
      default: function(){
        return ["流行","新款","精选"]
      }
    }
  },
  components:{
  },
  mounted() {

  },
  methods:{
    itemClick: function(index){
      this.currentIndex = index;
      this.$emit('tabClick',index);
    }
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
.tab-control {
  display: flex;
  text-align: center;
  line-height: 40px;
  font-size: 15px;
  background-color: #fff;
}
.tab-control-item {
  flex: 1;
}
.tab-control-item span {
  padding-bottom: 5px;
}
.active {
  color: var(--color-high-text);
}
.tab-control-item.active span {
  border-bottom: 2px solid var(--color-high-text);
}
</style>