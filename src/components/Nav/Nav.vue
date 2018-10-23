<template>
  <div class="nav">
      <router-link to='/goods' class='goods_item'>商品
        <i class="line"></i>
      </router-link>
      <router-link to='/ratings' class='goods_item'>评价
        <i class="line"></i>
      </router-link>
      <router-link to='/seller' class='goods_item'>商家
        <i class="line"></i>
      </router-link>
  </div>
</template>

<script>
export default {
  name: 'Nav',
  data () {
    return {
     
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nav{
    width:100%;
    height:40px;
    display:flex;
    border-bottom:1px solid #ddd;
}

.nav .goods_item{
    flex:1;
    font-size:13px;
    color:#666;
    line-height:40px;
    text-align:center;
    text-decoration:none;
    position:relative;
}

.nav .active{
    color:#ffbb22;
}

.nav .active .line{
    width:20px;
    height:1px;
    background:#ffbb22;
    position:absolute;
    bottom:0;
    left:50%;
    margin-left:-10px;
}
</style>
