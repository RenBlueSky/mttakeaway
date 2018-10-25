<template>
  <div class="goods">
      <div class="foods_wrapper">
        <!--左-->
        <div class="menu_box">
          ul
        </div>
        <!--右-->
        <div class="foods_box">

        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Goods',
  data(){
    return{
      special:{},
      foos:[]
    }
  },
  created(){
    fetch('/api/goods').then(res=>{
      return res.json()
    }).then(resp=>{
      if(resp.code===0){
        console.log(resp.data)
        console.log(resp.data.food_spu_tags)
        this.foods = resp.data.food_spu_tags
        this.special = resp.data.container_operation_source
      }
    })
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
  width:60px;
  height:100%;
  background:#f00;
}

.foods_wrapper .foods_box{
  flex:1;
  height:100%;
  background:#00f;
}
</style>
