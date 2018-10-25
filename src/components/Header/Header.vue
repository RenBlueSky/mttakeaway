<template>
  <div>
    <div class="header">
      <div class="top_box">
        <div class="iconfont arrow">&#xe602;</div>
        <div class="search_box">
          <span class="iconfont searchicon">&#xe696;</span>
          <input type="text" class="search" placeholder="搜索店内商品"/>
        </div>
        <div class="collage_box">
          <span class="collage">拼单</span>
          <span class="iconfont point">&#xe646;</span>
        </div>
      </div>

      <!--背景-->
      <div class="header_bg" :style="headerBg"></div>

      <!--header中部-->
      <div class="middle_box">
        <div class="m_bg" :style="mBg"></div>
        <div class="name">
          <h3>{{poiInfo.name}}</h3>
        </div>
        <div class="collect_box">
          <div class="iconfont star">&#xe603;</div>
          <div class="collect">收藏</div>
        </div>
      </div>

      <!--header底部-->
      <div class="notice_wrapper">
        <img v-if="poiInfo.discounts2" :src="poiInfo.discounts2[0].icon_url" class="notice_img"/>
        <span v-if="poiInfo.discounts2" class="notice">{{poiInfo.discounts2[0].info}}</span>
        <div v-if="poiInfo.discounts2" class="activity" v-on:click="showDetail">
          <span class="activity_count">{{poiInfo.discounts2.length}}个活动</span>
          <span class="iconfont count">&#xe647;</span>
        </div>
      </div>
    </div>
    <ActiviDetail :poiInfo="poiInfo" :isShowDetail="isShowDetail"></ActiviDetail>
  </div>
</template>

<script>
import ActiviDetail from "../ActiviDetail/ActiviDetail"

export default {
  data(){
    return {
      isShowDetail:false
    }
  },
  props:{
    poiInfo:{
      type:Object,
      default:{}
    }
  },
  created(){
    
  },
  computed:{
    headerBg(){
      return "background-image: url(" + this.poiInfo.head_pic_url + ");"
    },
    mBg(){
      return "background-image: url(" + this.poiInfo.pic_url + ");"
    }
  },
  methods:{
    showDetail(){
      this.isShowDetail = true
    },
  },
  components:{
    ActiviDetail
  }
}
</script>

<style scoped>
.header{
  height:160px;
  padding-top:20px;
  box-sizing:border-box;
  position:relative;
}

.header .top_box{
  height:30px;
  width:100%;
  display:flex;
  align-items:center;
}

.header .top_box .arrow{
  width:30px;
  font-size:20px;
  margin-left:10px;
  color:#fff;
}

.header .top_box .search_box{
  flex:1;
  padding:0 10px;
  position:relative;
}

.header .top_box .search_box .searchicon{
  position:absolute;
  left:16px;
  top:8px;
}

.header .top_box .search_box .search{
  width:100%;
  height:30px;
  border:0;
  box-sizing: border-box;
  background: #cdcdcc;
  border-radius: 25px;
  padding-left: 28px;
}

.header .top_box .collage_box{
  width:60px;
  margin-right:10px;
}

.header .top_box .collage_box .collage{
  font-size:12px;
  text-align:center;
  color:#fff;
  border:1px solid #fff;
  border-radius:2px;
  margin-right:10px;
}

.header .top_box .collage_box .point{
  color:#fff;
}

.header .header_bg{
  width:100%;
  height:160px;
  position:absolute;
  top:0;
  left:0;
  z-index:-1;
  background-size:100% 135%;
  background-position:center -12px;
}

.header .middle_box{
  padding:16px 10px 14px;
  height:50px;
}

.header .middle_box .m_bg{
  width: 50px;
  height: 50px;
  background-size: 135% 100%;
  background-position: center;
  border-radius: 5px;
  float: left;
}

.header .middle_box .name{
  float: left;
  padding: 18px 0 0 12px;
}

.header .middle_box .name h3{
  color:#fff;
} 

.header .middle_box .collect_box{
  float:right;
}

.header .middle_box .collect_box .star{
  color:#fff;
  font-size:20px;
}

.header .middle_box .collect_box .collect{
  color:#fff;
  font-size:10px;
}

.header .notice_wrapper{
  width:100%;
  display:flex;
  align-items:center;
  position:absolute;
  bottom:6px;
  left:0;
}

.header .notice_wrapper .notice_img{
  width:14px;
  height:14px;
  border-radius:2px;
  margin:0 4px;
}

.header .notice_wrapper .notice{
  flex:1;
  color:#fff;
  font-size:8px;
}

.header .notice_wrapper .activity{
  color:#fff;  
  text-align:center;
}

.header .notice_wrapper .activity .activity_count{
  font-size:8px;
}

.header .notice_wrapper .activity .count{
  font-size:8px;
  margin-right:4px;
}



</style>
