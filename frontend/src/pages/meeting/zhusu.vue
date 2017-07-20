<template>
<div class="container">
   <img src="../../assets/icon_zanwuxinxi@3x.png"></img>
   <p>暂无信息</p>
</div>
</template>

<script>  

export default {
    data() {
        return {
            notices: [],
            showPage:'',
        }
    },

    mounted() {
       
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
    },
}

</script>

<style lang="scss" scoped>
@import '../../style/mixin'; 
 .container{
     @include fj(center,column);
     img{
        height:2rem;
        margin-bottom: 0.5rem;
     }
     p{
         @include sc(0.58rem,#faa969);
     }
 }
</style>
