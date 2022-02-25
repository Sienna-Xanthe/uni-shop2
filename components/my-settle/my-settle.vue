<template>
  <view class="my-settle-container">
    <!-- 全选 -->
    <label class="radio" @click="changeAllState">
      <radio color="#C00000" :checked="isFullCheck"/><text>全选</text>
    </label>
    <!-- 合计 -->
    <view class="amount_box">
      合计：<text class="amount">￥{{checkGoodsAmount}}</text>
    </view>
    
    <!-- 结算按钮 -->
    <view class="btn-settle" @click="settlement">结算({{checkedCount}})</view>
    
  </view>
</template>

<script>
  import {mapGetters, mapMutations, mapState} from 'vuex'
  
  export default {
    name:"my-settle",
    data() {
      return {
        
      };
    },
    computed: {
      ...mapGetters('m_cart', ['checkedCount','total','checkGoodsAmount']),
      ...mapGetters('m_user', ['addstr']),
      ...mapState('m_user', ['token']),
      isFullCheck() {
        return this.total === this.checkedCount 
      }
    },
    methods: {
      ...mapMutations('m_cart',['updateAllGoodsState']),
      changeAllState() {
        this.updateAllGoodsState(!this.isFullCheck)
      },
      //用户点击了结算按钮
      settlement() {
        //1.
        if(!this.checkedCount) return uni.$showMsg('请选择要结算的商品！')
        //2.
        if(!this.addstr) return uni.$showMsg('请选择收货地址！')
        //3.
        if(!this.token) return uni.$showMsg('请先登录！')
      }
      
    }
  }
</script>

<style lang="scss">
.my-settle-container {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 50px;
  background-color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
  padding-left: 5px;
  
  .radio {
  display: flex;
  align-items: center;
}
.amount_box {
  .amount {
    color: #C00000;
    font-weight: bold;
  }
}
.btn-settle {
  background-color: #C00000;
  height: 50px;
  color: white;
  line-height: 50px;
  padding: 0 10px;
  min-width: 100px;
  text-align: center;
}
}


</style>
