<template>
    <div>
        <MyHeader />
        <div class="orderBox">
            <div class="row">
                <!-- 面包屑 -->
                <div class="crumbs">
                    <router-link  to="/">首页</router-link>
                    <div class="icon icon-right_s"></div>
                    <span class="">订单管理</span>
                </div>
                <div class="content">
                    <UserSide />
                    <div class="orderMain">
                        <NavTab :tabList="tabList" @Click="handleClick" :init='init' />
                        <div v-if="orderList.length != 0" class="orderContent">
                            <div class="item" v-for="(item,index) in orderList" :key='index'>
                                <div class="orderMian">
                                    <div class="itemHead">
                                        <div class="textInfo">
                                            <span class="time">下单时间：{{item.time}}</span>
                                            <span class="id">订单号：{{item.id}}</span>
                                        </div>
                                        <div class="delete icon icon-shanchu"></div>
                                    </div>
                                    <div class="itemMain">
                                        <div class="img">
                                            <router-link :to="'/detail?id='+item.goodId">
                                                <img :src="item.img" alt="">
                                            </router-link>
                                        </div>
                                        <router-link :to="'/detail?id='+item.goodId" class="name">
                                            {{item.name}}
                                        </router-link>
                                        <div class="number">
                                            包裹1
                                        </div>
                                        <div class="state">
                                            <div class="status">已取消</div>
                                            <!-- <div class="doBuy">再次购买</div> -->
                                        </div>
                                        <div class="price">
                                            <div class="mianPrice">￥719.20</div>
                                            <div class="otherPrice">（含运费：￥0.00元）</div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <VuePage :cur="cur" :all="all" :callback="callback" />
                        <NoData v-if="orderList.length == 0" position="0 -760px" />
                    </div>
                </div>
            </div>
        </div>
        <MyFooter />
    </div> 
</template>
<script>
import MyHeader from "@/components/MyHeader/MyHeader.vue";
import MyFooter from "@/components/MyFooter/MyFooter.vue";
import UserSide from "@/components/UserSide/UserSide.vue";
import NavTab from "@/components/navTab/navTab.vue";
import VuePage from "@/components/page/page.vue"

export default{
  components: {  MyHeader,  MyFooter ,UserSide,NavTab,VuePage}, 
    name:"userCollection",
    data(){
        return{
            cur: 1,
            all: 8,
            msg: '',
            tabList:['全部订单','待付款','待发货','已发货','待评价'],
            init:0,
            orderList:[
                {goodId:0,name:'男/女 轻柔色纺纱家居拖鞋',img:'https://yanxuan-item.nosdn.127.net/072a79db3d9e3f4a1d652f498311e102.png?quality=95&thumbnail=200x200&imageView',price:'43.9',id:'92093107',time:'2019-10-22 14:55:13',},
            ]
        }
    },
    created(){
        
    },
    mounted(){
        
    },
    methods:{
        callback(data) {
          this.cur = data
          this.msg = '你点击了'+data+ '页'
        },
        handleClose(e,i){
            this.collectionList.splice(i,1)
        },
        handleClick(i){
            if(i == this.init){
                return
            }
            this.init = i
        }
    },
}
</script>

<style lang="scss">
    .orderBox{
        .content{
            display: flex;
            .orderContent{
                margin-top: 20px;
            }
            
            .orderContent{
                .item{
                    border: 1px solid #e8e8e8;
                }
            }
            
            .orderMain{
                width: 890px;
                margin-left: 20px;
                overflow: hidden;
                .itemHead{
                    background-color: #f5f5f5;
                    height: 43px;
                    border-bottom: 1px solid #e8e8e8;
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    font-size: 12px;
                    .textInfo{
                        margin-left: 20px;
                        .id{
                            margin-left: 40px;
                        }
                    }
                    .delete{
                        margin-right: 20px;
                        cursor: pointer;
                    }
                }
                .itemMain{
                    text-align: center;
                    font-size: 14px;
                    display: flex;
                    padding: 20px 0;
                    align-items: center;
                    .img{    
                        margin-left: 20px;
                        img{
                            width: 100px;
                            height: 100px;
                            background-color: #f4f4f4;
                            margin-right: 10px;
                        }
                    }
                    .name{
                        margin-left: 10px;
                        width: 220px;
                        text-align: left;
                        overflow: hidden;
                        white-space: nowrap;
                        text-overflow: ellipsis;
                    }
                    .number{
                        width: 130px;
                        margin-left: 20px;
                        color:#999;
                    }
                    .state{
                        width: 130px;
                        .status{

                        }
                        .doBuy{
                            margin-top: 5px;
                            color:#69c;
                        }
                    }
                    .price{
                        flex: 2;
                        border-left: 1px solid #e8e8e8;
                        .mianPrice{
                            font-size: 14px;
                            font-weight: 700;
                        }
                    }
                }
            }
        }
    }
</style>

