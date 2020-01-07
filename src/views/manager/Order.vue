<template>
  <div class="order">
    <van-nav-bar title="我的订单" />
    <van-tabs v-model="active" color="#1659a0">
      <van-tab title="全部">
      </van-tab>
      <van-tab title="未开始">
      </van-tab>
      <van-tab title="进行中">
      </van-tab> 
      <van-tab title="已完成">
      </van-tab>
    </van-tabs>
    <div>
      <ul>
        <li ></li>
      </ul>
    </div>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import {get} from '../../http/axios'
export default {
  data(){
    return {
      active:0,
      orders:[]
    }
  },
  computed:{
    ...mapState("user",["info"])
  },
  created(){
    this.loadOrders();
  },
  methods:{
    //加载我的订单
    loadOrders(){
      let url="order/query?customerId="+this.info.id;
      get(url).then((response)=>{
        this.orders=response.data;
      })
    }
  }
}
</script>
<style scoped>
.order {
  background: #f1f1f1;
}
</style>