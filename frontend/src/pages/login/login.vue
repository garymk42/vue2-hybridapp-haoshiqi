<template>
<div> 
    <div >
        <div class="top_view">
            <p class="r1">欢迎您使用会议记录软件！</p>
            <p class="r2">Welcome you to use the meeting record software！</p>
        </div>
        <div class="login_item">
            <p>账号</p>
            <input v-model="username"></input>
        </div>
        <div class="login_item">
            <p>密码</p>
            <input type="password" v-model="password"></input>
        </div>
        <div class="login_btn" @click="login">
            登录
        </div>
        <div class="error_view">
            密码输入错误
        </div>
        <div class="foot_view">
            欢迎使用会议接待系统
        </div>
    </div>
</div>
</template>

<script>  
export default {
    data() {
        return {
            showChild:false,
            username:"",
            password:"",
        }
    },
    components:{ 
    },
    mounted() {

    },
    methods: {
        login(){
            this.showChild = true;
            this.$emit('changeComponent','home');
        },
    },
}

</script>

<style lang="scss" scoped>
@import '../../style/mixin';
.top_view {
    height: 5.39rem;
    background: url('../../assets/bg_denglu.png') no-repeat 0 0;
    background-size: cover;
    @include fj;
    flex-direction: column;
    padding-left: 0.82rem;
    align-items: flex-start;
    .r1 {
        margin: 0px;
        padding: 0px;
        margin-top: 2.5rem;
        @include sc(0.48rem, white);
    }
    .r2 {
        @include sc(0.36rem, white);
        margin: 0px;
        padding: 0px;
        margin-bottom: 1.82rem;
    }
}

.login_item {
    @include fj;
    padding-top:0.42rem;
    margin-bottom:0.11rem;
    height: 1.62rem;
    margin-left: 0.82rem;
    margin-right: 0.82rem;
    align-items: center;
    border-bottom: 1px solid $blue;
    p {
        @include sc(0.52rem, $blue);
        margin-right:0.67rem;
    }
    input {
        flex:1;
            outline: none;
            @include sc(0.48rem, $defaultGrey);
            border: 0;
        }
}
.login_btn{
    height:1.37rem;
    margin-top:0.9rem;
    text-align: center;
    background-color:$mainBlue;
            @include sc(0.48rem, white);
    line-height: 1.37rem;
    margin-left: 0.72rem;
    margin-right: 0.72rem;
    border-radius:0.1rem;
}
.error_view{
    margin-top:0.69rem;
    @include  sc(0.42rem,$orange);
    text-align: center;
}
.foot_view{
    position: absolute;
    bottom:0.93rem;
    width:100%;
    @include  sc(0.42rem,#91959e);
    text-align: center;
}
</style>
