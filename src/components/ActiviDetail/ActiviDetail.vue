<template>
    <div>
    <!--活动详情蒙版-->
      <div class="detail_box" v-if="isShowDetail">
        <div class="detail_bg" :style="detailBg">
          <div class="detail_mbg" :style="detailmBg"></div>
          <div class="detail_name">{{poiInfo.name}}</div>
          <div class="star"></div>
          <div class="give_box">
            <span class="takeoff">{{poiInfo.min_price_tip}}</span>
            <i>|</i>
            <span class="takeoff">{{poiInfo.shipping_fee_tip}}</span>
            <i>|</i>
            <span class="takeoff">{{poiInfo.delivery_time_tip}}</span>
          </div>
          <div class="give_time">
              配送时间：{{poiInfo.shipping_time}}
          </div>
          <div class="detail_activity">
            <p>
                <img :src="poiInfo.discounts2[0].icon_url" class="detail_img"/>
                <span class="detail_ac">{{poiInfo.discounts2[0].info}}</span>
            </p>
          </div>
        </div>
        <div class="close" @click="hiddenDetail">
          <span class="iconfont iconclose">&#xe6e7;</span>
        </div>
      </div>
    </div>
</template>

<script>
export default {
    data(){
        return {

        }
    },
    props:{
        poiInfo:{
            type:Object,
            default:{}
        },
        isShowDetail:{
            type:Boolean,
            default:false
        }
    },
    computed:{
        detailBg(){
            return "background-image:url(" + this.poiInfo.poi_back_pic_url + ")"
        },
        detailmBg(){
            return "background-image: url(" + this.poiInfo.pic_url + ");"
        }
    },
    methods:{
        hiddenDetail(){
            this.isShowDetail  = false
        }
    }
}
</script>

<style>
/*活动详情*/
.detail_box{
  width:100%;
  height:100%;
  position:absolute;
  top:0;
  left:0;
  z-index:10;
  padding:30px 20px 60px 30px;
  box-sizing:border-box;
  background: rgba(0,0,0,0.3);
  color:#fff;
}

.detail_box .detail_bg{
  width: 100%;
  height: 100%;
  background-size: 135% 100%;
  background-position: center;
  border-radius: 5px;
  display:flex;
  align-items:center;
  flex-direction:column;
}

.detail_box .detail_bg .detail_mbg{
    width:80px;
    height:80px;
    background-size:100% 100%;
    background-position:center;
    border-radius:4px;
    margin-top:40px;
}

.detail_box .detail_bg .detail_name{
    margin-top:16px;
}

.detail_box .detail_bg .star{
    margin-top:10px;
}

.detail_box .detail_bg .give_box{
    margin-top:10px;
    font-size:10px;
    color:#888;
}

.detail_box .detail_bg .give_box .takeoff,
.detail_box .detail_bg .give_box i{
    margin-right:20px;
}


.detail_box .detail_bg .give_time{
    margin-top:10px;
    font-size:10px;
    color:#888;
}

.detail_box .detail_bg .detail_activity{
    margin-top:30px;
    height:16px;
    padding:0 20px;
}

.detail_box .detail_bg .detail_activity p {
    border-top:1px solid #bababc;
    padding-top:20px;
}

.detail_box .detail_bg .detail_activity p .detail_img{
    width:16px;
    height:16px;
    border-radius:2px;
    vertical-align: middle;
} 

.detail_box .detail_bg .detail_activity p .detail_ac{
    display:inline-block;
    line-height:16px;
    font-size:12px;
} 

.detail_box .close{
    width:22px;
    height:22px;
    border-radius:50%;
    position:absolute;
    left:50%;
    bottom:18px;
    margin-left:-13px;
    border:1px solid #eee;
}

.detail_box .close .iconclose{
   font-size:21px;
}
</style>


