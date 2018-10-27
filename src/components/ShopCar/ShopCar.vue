<template>
    <div class="shopcar_wrapper">
        <div class="carlist_box">
            <div class="new">新用户立减20元</div>
            <div class="clear_box">
                <div class="pocket">1号口袋</div>
                <div class="clear">
                    <span class="iconfont">&#xe6bf;</span>
                    清空购物车
                </div>
            </div>
            <ul>
                <li class="carlist">
                    <div class="fooddname_box">
                        <p class="name">脆香油条</p>
                        <p class="unit">例</p>
                    </div>
                    <div class="carprice">
                        ￥6
                    </div>
                    <div class="contron_box">
                        <NumControl></NumControl>
                    </div>
                </li>
            </ul>
        </div>

        <div class="car_box">
            <div class="icon_box"  :class="{'active':totalnum>0}">
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

        }
    },
    components:{
        NumControl
    },
    computed:{
        totalprice(){
            let totalprice = 0;
            this.foodschangeArr.forEach((item,index)=>{
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
    bottom:0;
    left:0;
}

.shopcar_wrapper .carlist_box{
    width:100%;
    max-height:300px;
    position:absolute;
    top:-300px;
    left:0;
    background:#fff;
}

.shopcar_wrapper .carlist_box .new{
    width:100%;
    height:30px;
    line-height:30px;
    text-align:center;
    font-size:14px;
    background:#ddd;
}

.shopcar_wrapper .carlist_box .clear_box{
    width:100%;
    height:20px;
    background:#eee;
}

.shopcar_wrapper .carlist_box .clear_box .pocket{
    float:left;
    margin-left:4px;
}

.shopcar_wrapper .carlist_box .clear_box .clear{
    float:right;
    margin-right:4px;
}

.shopcar_wrapper .carlist_box ul{
    width:100%;
}

.shopcar_wrapper .carlist_box .carlist{
    display:flex;
    padding:6px 10px;
}

.shopcar_wrapper .carlist_box .carlist .fooddname_box{
    flex:1;
}

.shopcar_wrapper .carlist_box .carlist .fooddname_box .name{
    font-size:14px;
}

.shopcar_wrapper .carlist_box .carlist .fooddname_box .unit{
    font-size:12px;
    color:#999;
}

.shopcar_wrapper .carlist_box .carlist .carprice{
    width:60px;
}

.shopcar_wrapper .carlist_box .carlist .contron_box{
    width:60px;
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
