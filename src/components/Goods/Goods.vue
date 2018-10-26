<template>
  <div class="goods">
      <div class="foods_wrapper">
        <!--左菜单-->
        <div class="menu_box" ref="menuScroll">
          <ul>
            <li class="menu_item" :class="{'current':currentIndex===0}" v-on:click="chooseMenu(0)">
              <p class='item'>
                <img :src="special.tag_icon" v-if="special.tag_icon">
                {{special.tag_name}}
              </p>
            </li>

            <li class="menu_item" v-for="(item,index) in foods" :key="index" :class="{'current':currentIndex===index+1}" v-on:click="chooseMenu(index+1)">
              <p class='item'>
                <img :src="item.icon" v-if="item.icon">
                {{item.name}}
              </p>
            </li>
          </ul>
        </div>
        <!--右列表-->
        <div class="foods_box" ref="foodScroll">
          <ul>
            <li class="specali_img foodli">
              <div class="specail_imgbox" v-for="(item,index) in special.operation_source_list" :key="index">
                 <img :src="item.pic_url">
              </div>
            </li>
            <!--food-->
            <li class="list_box foodli" v-for="(item,index) in foods" :key="index">
              <h4 class="title">{{item.name}}</h4>
              <ul>
                <li class="food_item" v-for="(food,foodi) in item.spus" :key="foodi">
                  <div class="icon" :style="headBg(food.picture)"></div>
                  <div class="content">
                    <h3 class="name">{{food.name}}</h3>
                    <p class="desc" v-if="food.description">{{food.description}}</p>
                    <div class="extra">
                      <span class="saled">{{food.month_saled_content}}</span>
                      <span class="praise">{{food.praise_content}}</span>
                    </div>
                    <img class="product" :src="food.product_label_picture" v-if="food.product_label_picture">
                    <p class="price">
                      <span class="text">￥{{food.min_price}}</span>
                      <span class="unit">/{{food.unit}}</span>
                    </p>
                  </div>
                  <div class="num_box">
                    <NumControl :food="item"></NumControl>
                  </div>
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <ShopCar :poiInfo="poiInfo"></ShopCar>
      </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
import ShopCar from "../ShopCar/ShopCar"
import NumControl from "../NumControl/NumControl"

export default {
  name: 'Goods',
  data(){
    return{
      special:{},
      poiInfo:{},
      foods:[],
      foodHeight:[],
      MNScroll:{},
      FDScroll:{},
      scrY:0
    }
  },
  components:{
    ShopCar,
    NumControl
  },

  created(){
    fetch('/api/goods').then(res=>{
      return res.json()
    }).then(resp=>{
      if(resp.code===0){
        console.log(resp.data)
        console.log(resp.data.food_spu_tags)
        this.poiInfo = resp.data.poi_info
        this.foods = resp.data.food_spu_tags
        this.special = resp.data.container_operation_source
        //滚动
        this.$nextTick(()=>{ //vue自带方法dom渲染完成
          this.initScroll();
          this.getHeight();
        })
      }
    })
  },

  methods:{
    headBg(pic){
      return "background-image: url(" + pic + ");"
    },
    initScroll(){
      this.MNScroll = new BScroll(this.$refs.menuScroll,{click: true})
      this.FDScroll = new BScroll(this.$refs.foodScroll,{probeType:3})
      this.FDScroll.on('scroll',(scr)=>{
        this.scrY = Math.abs(scr.y)
      })
    },
    getHeight(){
      let num = 0;
      let foodli = this.$refs.foodScroll.getElementsByClassName("foodli")
      let height = 0
      this.foodHeight.push(height)
      for(let i = 0; i<foodli.length; i++){
        height += foodli[i].clientHeight
        this.foodHeight.push(height)
      }
        console.log(this.foodHeight)
    },
    chooseMenu(i){
      console.log(i)
      let foodli = this.$refs.foodScroll.getElementsByClassName("foodli")
      let foodEle = foodli[i]
      this.FDScroll.scrollToElement(foodEle,300)
      
      //console.log(foodEle)
    }
  },

  computed:{
    currentIndex(){
      for(let i=0; i<this.foodHeight.length; i++){
        if((this.scrY>=this.foodHeight[i] && this.scrY<=this.foodHeight[i+1]) || !this.foodHeight[i+1]){
          return i
        }
      }
      return 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.foods_wrapper{
  width:100%;
  display:flex;
  position:absolute;
  top:200px;
  bottom:51px;
  overflow:hidden;
}

.foods_wrapper .menu_box{
  width:85px;
  height:100%;
  background:#ccc;
}

.foods_wrapper .menu_box .menu_item.current{
  background:#eee;
}

.foods_wrapper .menu_box .menu_item{
  padding:15px 23px 13px 10px;
  border-bottom:1px solid #e4e4e4;
}

.foods_wrapper .menu_box .menu_item .item{
  font-size:13px;
  color:#333333;
  line-height:18px;
  vertical-align:middle;
  display:-webkit-box;
  -webkit-box-orient:vertical;
  -webkit-line-clamp:2;
  overflow:hidden;
}

.foods_wrapper .menu_box .menu_item .item img{
  width:15px;
  height:15px;
  vertical-align:middle;
}

.foods_wrapper .foods_box{
  flex:1;
}

.foods_wrapper .foods_box .specali_img{
  padding:11px 11px 0 11px;
  border-bottom:1px solid #e4e4e4;
}

.foods_wrapper .foods_box .specali_img img{
  width:100%;
  margin-bottom:11px;
  border-radius:5px;
}

.foods_wrapper .foods_box .list_box{
  padding:5px 8px 6px 6px;
}

.foods_wrapper .foods_box .list_box .title{
  font-weight:600;
}

.foods_wrapper .foods_box .list_box .food_item{
  display:flex;
  padding:8px 10px;
  position:relative;
}

.foods_wrapper .foods_box .list_box .food_item .icon{
  width:63px;
  background-position:center;
  background-size:120% 100%;
  background-repeat:no-repeat;
  margin-right:11px;
  height:75px;
}

.foods_wrapper .foods_box .list_box .food_item .content{
  flex:1;
}

.foods_wrapper .foods_box .list_box .food_item .content .name{
  font-size:16px;
}

.foods_wrapper .foods_box .list_box .food_item .content .desc{
  font-size:12px;
  color:#999;
   display:-webkit-box;
  -webkit-box-orient:vertical;
  -webkit-line-clamp:1;
  overflow:hidden;
  margin-top:6px;
}

.foods_wrapper .foods_box .list_box .food_item .content .extra{
  color:#999;
  font-size:12px;
  margin-top:10px;
}

.foods_wrapper .foods_box .list_box .food_item .content .extra .saled{
  margin-right:14px;
}

.foods_wrapper .foods_box .list_box .food_item .content .product{
  width:60px;
  height:16px;
  border-radius:2px;
  margin-top:8px;
}


.foods_wrapper .foods_box .list_box .food_item .content .price{
  font-size:13px;
  margin-top:8px;
}

.foods_wrapper .foods_box .list_box .food_item .content .price .text{
  color:#be2c2c;
}

.foods_wrapper .foods_box .list_box .food_item .content .price .unit{
  color:#999;
}

.foods_wrapper .foods_box .list_box .food_item .num_box{
  position:absolute;
  right:0;
  bottom:0;
}

li{
    list-style:none;
}


</style>
