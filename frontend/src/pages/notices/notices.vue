<template>
<div>
    <div class="container">
        <div class="header_view">
            <div class="back_btn" @click="jumpTo('home')"></div>
            <p>消息</p>
            <div class="right_btn"></div>
        </div>  
        <div class="body_view">
        <!--<section class="item_view" v-for="notice in notices" @click="jumpToMeeting(notice)">
        {{notice.name}}
        </section>-->
        </div>
    </div>
</div>
</template>

<script> 
import moment from 'moment' 
export default {
    data() {
        return {
            notices: [],
        }
    },

    mounted() {
        this.notices = [{
            name:'B101会议室',
            dateText:'2017.5.17-5.19',
        },{
            name:'A101会议室',
            dateText:'2017.5.17-5.19',
        }];
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
    },
}

</script>

<style lang="scss" scoped>
@import '../../style/mixin'; 

.container {
    background-color: white;
    height: 100vh;
    @include fj(flex-start,column,center);
    z-index:1;
}


.header_view {
    background-color:$mainBlue;
    @include fj;
    flex: 0 0 1.44rem;
    height: 1.44rem;
    width:100%;
    p {
        @include sc(0.54rem, white);
    }
    .back_btn {
         margin-left: 0.32rem;
        background: url(../../assets/button_back@3x.png) no-repeat 0 0;
        background-size: contain;
        height: 0.6rem;
        width: 0.6rem;
    }

    .right_btn {
        margin-right: 0.32rem;
        height: 0.6rem;
        width: 0.6rem;
    }
   
}

.body_view{
    @include fj(flex-start,column);
    flex:1;
    width:100%;
    margin-top:0.3rem;
    background:url(../../assets/icon_zanwuxinxi@3x.png)  2rem 2rem no-repeat;
    background-position-x: center;
    background-position-y: center;
    .item_view{
        background:url(../../assets/icon_zanwuxinxi@3x.png) no-repeat ;
        background-size:contain;
        // width:10.32rem;
        // height:3.14rem;
        // box-shadow: 5px 5px 5px  #888888;
        margin-bottom:0.24rem;
    }
}
</style>
