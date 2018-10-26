<template>
    <div class="numcontrol_wrapper">
        <div class="delet" v-on:click.native="deletClick">
            <span class="iconfont icondelet">&#xe636;</span>
        </div> 
        <div class="num">2</div>
        <div class="add" v-on:click.native="addClick">
            <span class="iconfont iconadd">&#xe6e7;</span>
        </div>
    </div>
</template>


<script>
export default {
    name:"Num",
    props:{
        food:{
            type:Object,
            default:{}
        }
    },
    created(){
        
    },
    methods:{
        deletClick(){
            console.log(this.food)
        },
        addClick(){
            console.log(0)
        }
    }
}
</script>


<style>
.numcontrol_wrapper .delet,
.numcontrol_wrapper .num,
.numcontrol_wrapper .add{
    display:inline-block;
}

.numcontrol_wrapper .delet{
    width:16px;
    height:16px;
    border-radius:50%;
    border:1px solid #aaa;
}

.numcontrol_wrapper .delet .icondelet{
    font-size:12px;
    color:#aaa;
}

.numcontrol_wrapper .add{
    width:16px;
    height:16px;
    border-radius:50%;
    background:#fc0;
}

.numcontrol_wrapper .add .iconadd{
    font-size:10px;
    font-weight:600;
    color:#000;
    display:inline-block;
    text-align:center;
    vertical-align: middle;
    line-height:16px;
}

.numcontrol_wrapper .num{
    margin:0 2px;
}
</style>
