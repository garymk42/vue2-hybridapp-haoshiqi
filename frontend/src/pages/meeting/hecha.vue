<template>
<div class="container">
   <section class="item" v-for="item in list" @click="onClick(item)">
   <img v-show="!item.checked" src="../../assets/button_gou_m@3x.png"></img>
   <img v-show="item.checked" src="../../assets/button_gou_x@3x.png"></img>
   <p :class="{'checked':item.checked,'unchecked':!item.checked}">{{item.name}}</p>
   </section>
</div>
</template>

<script>  

export default {
    data() {
        return {
            list:[],
        }
    },

    mounted() {
       this.list = [{
        name:'确认食宿用车',
        checked:false,
       },{
        name:'邀请所有参会人员',
        checked:false,
       },{
        name:'会前准备确认',
        checked:false,
       },{
        name:'上传照片',
        checked:false,
       },{
        name:'上传录音',
        checked:false,
       },{
        name:'提醒人员按时参会',
        checked:false,
       },{
        name:'确认参会人员',
        checked:false,
       },];
    },

    components: {
      
    },
    methods: {
         jumpTo(componentName){
            this.$emit('changeComponent',componentName);
        },
        jumpToMeeting(obj){
            // this.jumpTo('meeting');
        },
        onItemClick(componentName){
            this.showPage = componentName;
        },
        onClick(obj){
            let arr = [];
            this.list.forEach((item)=>{
                if(item.name == obj.name)
                    item.checked = !item.checked;
                arr.push(item);
            });
            this.list = arr;
        }
    },
}

</script>

<style lang="scss" scoped>
@import '../../style/mixin'; 
.container{
    @include fj(flex-start,column);
    margin-top:0.24rem;
    
        width:100%;
    .item{
        @include fj(flex-start,row);
        background:url(../../assets/button_bg@3x.png) no-repeat;
        height:1.41rem;
        font-size:0.48rem;
        width:95%;
        box-shadow: 2px 2px 2px #e0e0e0;
        margin-left:0.24rem;
        margin-right:0.24rem;
        margin-bottom:0.24rem;
        img{
            margin-left:0.56rem;
            margin-right:0.3rem;
            height:0.5rem;
            width:0.5rem;
        }
        .checked{
            text-decoration:line-through;
            color:#90949d;
        }
        .unchecked{
            color:#585d6a;
                text-decoration:none;
        }
    }
}
</style>
