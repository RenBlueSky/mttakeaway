<template>
    <transition name="detail_transition">
        <div class="fooddetail_wrapper">
            <div class="food_box">
                <div class="top_box">
                    <span class="iconfont del">x</span>
                    <span class="iconfont point">...</span>
                    <span class="iconfont share">享</span>  
                </div>
                <div class="foodimg">
                    <img src="" alt="">
                </div>
                <div class="detail_box">
                    <div class="detail">
                        <div>麦辣鸡翅</div>
                        <div>月售420块</div>
                        <div>￥22/例</div>
                    </div>
                    <div class="choose">选规格</div>
                </div>
            </div>
            <div class="line"></div>
            <div class="rating_box">

            </div>
        </div>
    </transition>
</template>

<script>
export default {
    props:{
        foodDetail:{
            type:Object,
            default:{}
        }
    }
}
</script>


<style>
.fooddetail_wrapper{
    width:100vw;
    background:#fff;
    position:fixed;
    top:0;
    left:0;
    z-index:9;
    bottom:51px;
}

.fooddetail_wrapper .food_box{
    width:100%;
    height:300px;
}

.fooddetail_wrapper .food_box .top_box{
    height:20px;
}

.fooddetail_wrapper .food_box .top_box .del{
    height:20px;
    width:20px;
    display:inline-block;
    background:#666;
    border-radius:50%;
    color:#fff;
    line-height:20px;
    text-align:center;
}

.fooddetail_wrapper .food_box .top_box .share{
    height:20px;
    width:20px;
    display:inline-block;
    background:#666;
    border-radius:50%;
    color:#fff;
    font-size:12px;
    float:right;
    line-height:20px;
    text-align:center;
    margin-right:12px;
}

.fooddetail_wrapper .food_box .top_box .point{
    height:20px;
    width:20px;
    display:inline-block;
    background:#666;
    border-radius:50%;
    color:#fff;
    float:right;
    line-height:20px;
    text-align:center;
    margin-right:16px;
}

.fooddetail_wrapper .food_box .foodimg{
    width:100%;
    height:30vh;
    background:#f00;
}
</style>
