<template>
    <div class="shopcar_wrapper">
        <div class="car_box">
            <div class="icon_box">
                <span class="iconfont iconcar">&#xe601;</span>
            </div>
            <div class="should_box">
                <p>另需{{poiInfo.shipping_fee_tip}}</p>
            </div>
        </div>
        <div class="start_box">
            {{poiInfo.min_price_tip}}
        </div>
    </div>
</template>


<script>
export default {
    props:{
        poiInfo:{
            type:Object,
            default:{}
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
    bottom:0;
    left:0;
}

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

.shopcar_wrapper .car_box .icon_box .iconcar{
    font-size:20px;
    position:absolute;
    top:10px;   
    left:10px;
    color:#eee;
}

.shopcar_wrapper .car_box .should_box{
    font-size:14px;
    position:absolute;
    top:14px;   
    left:70px;
    color:#eee;
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
