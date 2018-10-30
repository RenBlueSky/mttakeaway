<template>
    <div class="shopcar_wrapper">
        <div class="carlist_box" v-if="showCarList" :class="{'show':showCarList}">
            <div class="new" v-if="poiInfo.discounts2[0].info">{{poiInfo.discounts2[0].info}}</div>
            <div class="clear_box">
                <div class="pocket">1号口袋</div>
                <div class="clear">
                    <span class="iconfont">&#xe6bf;</span>
                    清空购物车
                </div>
            </div>
            <ul ref="carlistscr">
                <li class="carlist" v-for="(item,index) in foodschangeArr" :key="index">
                    <div class="fooddname_box">
                        <p class="name">{{item.name}}</p>
                        <p class="unit" v-if="!item.description">{{item.unit}}</p>
                        <p class="description" v-if="!item.unit">{{item.description}}</p>
                    </div>
                    <div class="carprice">
                        ￥{{item.min_price}}
                    </div>
                    <div class="contron_box">
                        <NumControl class="ctr"></NumControl>
                    </div>
                </li>
            </ul>
        </div>

        <div class="car_box">
            <div class="icon_box"  :class="{'active':totalnum>0}" @click="carClick">
                <i v-if="totalnum">{{totalnum}}</i>
                <span class="iconfont iconcar"  :class="{'active':totalnum>0}">&#xe601;</span>
            </div>
            <div class="should_box">
                <p class="price" v-if="totalprice">￥{{totalprice}}</p>
                <p class="other">另需{{poiInfo.shipping_fee_tip}}</p>
            </div>
        </div>
        <div class="start_box" :class="{'active':totalnum>0}">
            {{paystatus}}
        </div>
    </div>
</template>


<script>
import NumControl from "../NumControl/NumControl"
import BScroll from "better-scroll"

export default {
    props:{
        poiInfo:{
            type:Object,
            default:{}
        },
        foodschangeArr:{
            type:Array,
            default:[]
        }
    },
    data(){
        return {
            showCarList:false
        }
    },
    components:{
        NumControl
    },
    computed:{
        totalprice(){
            let totalprice = 0;
            this.foodschangeArr.forEach((item,index)=>{
                console.log(item)
                totalprice += item.min_price*item.count
            })
            return totalprice
        },
        totalnum(){
            let num = 0;
            this.foodschangeArr.forEach((item,index)=>{
                num += item.count
            })
            return num
        },
        paystatus(){
            if(this.totalnum>0){
                return "去结算"
            }else{
                return this.poiInfo.min_price_tip
            }
        },
    },
    methods:{
        carClick(){
            if(!this.totalnum){
                return false
            }else{
                this.showCarList = !this.showCarList
                this.$nextTick(()=>{ //dom已经渲染
                    if(!this.carScroll){
                        this.carScroll = new BScroll(this.$refs.carlistscr,{click:true})
                    }
                })
            }
        }
    }
}
</script>


<style>
.shopcar_wrapper{
    display:flex;
    height:51px;
    width:100%;
    background:rgba(100,100,100,0.8);
    position:fixed;
    z-index:100;
    bottom:0;
    left:0;
}

.shopcar_wrapper .carlist_box{
    width:100%;
    max-height:300px;
    position:absolute;
    top:0;
    left:0;
    z-index:-100;
}

.shopcar_wrapper .carlist_box.show{
    transform:translateY(-100%);
}

.shopcar_wrapper .carlist_box .new{
    width:100%;
    height:30px;
    line-height:30px;
    text-align:center;
    font-size:12px;
    background:rgb(242, 247, 173);
}

.shopcar_wrapper .carlist_box .clear_box{
    width:100%;
    height:20px;
    padding:4px 0;
    background:#eee;
}

.shopcar_wrapper .carlist_box .clear_box .pocket{
    float:left;
    margin-left:4px;
    font-size:12px;
}

.shopcar_wrapper .carlist_box .clear_box .clear{
    float:right;
    margin-right:4px;
    font-size:12px;
}

.shopcar_wrapper .carlist_box ul{
    width:100%;
    display:inline-block;
    overflow:hidden;
    max-height:250px;
    background: #fff;
}

.shopcar_wrapper .carlist_box .carlist{
    display:flex;
    padding:6px 10px;
    position:relative;
    border-bottom:1px solid #ddd;
}

.shopcar_wrapper .carlist_box .carlist .fooddname_box{
    flex:1;
}

.shopcar_wrapper .carlist_box .carlist .fooddname_box .name{
    font-size:14px;
    margin-top:2px;
}

.shopcar_wrapper .carlist_box .carlist .fooddname_box .unit{
    font-size:12px;
    color:#999;
    margin-top:3px;
}

.shopcar_wrapper .carlist_box .carlist .fooddname_box .description{
    font-size:12px;
    color:#999;
    margin-top:3px;
}

.shopcar_wrapper .carlist_box .carlist .carprice{
    width:60px;
    line-height:38px;
}

.shopcar_wrapper .carlist_box .carlist .contron_box{
    width:70px;
}

.shopcar_wrapper .carlist_box .carlist .contron_box .ctr{
    top:15px;
    position:absolute;
    right:10px;
}

/**/
.shopcar_wrapper .car_box{
    flex:1;
}

.shopcar_wrapper .car_box .icon_box{
    width:40px;
    height:40px;
    background:#8f8f8f;
    border-radius:50%;
    position:absolute;
    top:-14px;   
    left:20px;
}

.shopcar_wrapper .car_box .icon_box i{
    display:inline-block;
    width:16px;
    height:16px;
    background:#f00;
    color:#fff;
    font-size:12px;
    text-align:center;
    line-height:16px;
    border-radius:50%;
    position:absolute;
    right:-6px;
    top:1px;
}

.shopcar_wrapper .car_box .icon_box .iconcar{
    font-size:20px;
    position:absolute;
    top:10px;   
    left:10px;
    color:#eee;
}

.shopcar_wrapper .car_box .should_box{
    position:absolute;
    top:12px;   
    left:60px;
}

.shopcar_wrapper .car_box .should_box .price{
    font-size:16px;
    color:#fff;
}

.shopcar_wrapper .car_box .should_box .other{
    font-size:12px;
    color:#ddd;
    margin-top:4px;
}


.shopcar_wrapper .start_box{
    width:86px;
    font-size:16px;
    text-align:center;
    line-height:51px;
    color:#eee;
}

.shopcar_wrapper .car_box .icon_box.active,
.shopcar_wrapper .start_box.active{
    background:#fc0;
}
.shopcar_wrapper .car_box .icon_box .iconcar.active{
    color:#333;
}
.shopcar_wrapper .start_box.active{
    color:#000;
}

</style>
