<template>
    <div class="numcontrol_wrapper">
        <transition name="move">
            <div class="delet" @click="deletClick" v-if="food.count">
                <span class="iconfont icondelet">&#xe636;</span>
            </div> 
        </transition>
            <div class="num" v-if="food.count">{{food.count}}</div>
        
        <div class="add" @click="addClick">
            <span class="iconfont iconadd">&#xe6e7;</span>
        </div>
    </div>
</template>


<script>
import Vue from "vue"

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
            this.food.count --
        },
        addClick(){
            if(this.food.count){
                this.food.count ++
            }else{
                Vue.set(this.food,"count",1)
            }

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
    display:inline-block;
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

.move-enter-active,.move-leave-active{
    transition:all 0.5s linear;
}

.move-enter,.move-leave-to{
    transform:translateX(20px) rotate(180deg);
}

.numcontrol_wrapper .num{
    margin:0 2px;
}
</style>
