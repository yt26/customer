<template>
    <briup-fulllayout title="常用地址">
    <!-- {{addresses}} -->
    {{info}}
    <van-list>
        <van-cell
            v-for="item in addresses"
            :key="item.id"
            :title="item.province+''+item.city+''+item.area+''+item.address"
        />
    </van-list>
    <br>
    <van-button block type="default" @click="toAddressEditHandler">
        添加
    </van-button>
    </briup-fulllayout>
</template>
<script>
import { get } from "../../../http/axios";
import {mapState} from "vuex"
export default{
    data(){
        return{
            addresses:[]
        }
    },
    computed:{//计算属性
        //将状态机中user对象中的info对象获取到
        ...mapState("user",["info"])
    },
    created(){
        this.loadAddress();
    },
    methods:{
        loadAddress(){
            let id=this.info.id;
            let url="http://localhost:6677/address/findByCustomerId?id="+id;
            get(url).then((Response)=>{
                this.addresses=response.data;
            })
        },
        //跳转到编辑页面的
        toAddressEditHandler(){
            //编程跳转
            this.$router.push("/manager/address_edit");
        }
    }
}
</Script>
<style  scoped>
   
</style>