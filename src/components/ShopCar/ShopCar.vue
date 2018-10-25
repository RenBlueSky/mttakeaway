<template>
    <div class="shopcar_wrapper">
        <div class="car_box">
            <div class="icon_box">
                <span class="iconfont"></span>
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
    background:#999;
    position:fixed;
    bottom:0;
    left:0;
}

.shopcar_wrapper .car_box{
    flex:1;
}

.shopcar_wrapper .car_box .icon_box{

}
</style>
