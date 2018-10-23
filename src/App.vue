<template>
  <div id="app">
    <Header :poiInfo="poiInfo"></Header>
    <Nav></Nav>
    <router-view/>
  </div>
</template>

<script>
import Header from './components/Header/Header'
import Nav from './components/Nav/Nav'

export default {
  name: 'App',
  components:{
    Header,
    Nav
  },
  data(){
    return{
      poiInfo:{}
    }
  },
  created(){
    fetch('/api/goods').then(res=>{
      return res.json()
    }).then(resp=>{
      if(resp.code===0){
        console.log(resp.data.poi_info)
        this.poiInfo = resp.data.poi_info
      }
    })
  }
}
</script>

<style>

</style>
