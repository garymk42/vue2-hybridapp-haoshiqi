<template>
    <div>
        <div class="container">
            <div class="header_view">
                <div class="back_btn" @click="jumpTo('home')"></div>
                <p>公司章程会议详情</p>
                <div class="right_btn"></div>
            </div>
            <tab bar-active-color="#3e637c" active-color="#585d6a" defaultColor="#90949d"   custom-bar-width="2rem" class="tab">
                <tab-item selected @on-item-click="onItemClick('hecha')">核查清单</tab-item>
                <tab-item @on-item-click="onItemClick('laifang')">来访人员</tab-item>
                <tab-item @on-item-click="onItemClick('huichang')">会场信息</tab-item>
                <tab-item @on-item-click="onItemClick('zhusu')">住宿信息</tab-item>
            </tab>
    
            <div class="body_view">
                <Hecha v-show="showPage=='hecha'" />
                <Laifang v-show="showPage=='laifang'" />
                <Huichang v-show="showPage=='huichang'" />
                <Zhusu v-show="showPage=='zhusu'" />
            </div>
    
        </div>
    </div>
</template>

<script> 
import moment from 'moment';
import { Tab, TabItem, Sticky, Divider, XButton, Swiper, SwiperItem } from 'vux'
import Hecha from './hecha';
import Huichang from './huichang';
import Zhusu from './zhusu';
import Laifang from './laifang';
export default {
    data() {
        return {
            notices: [],
            showPage: 'hecha',
        }
    },

    mounted() {
        this.notices = [{
            name: 'B101会议室',
            dateText: '2017.5.17-5.19',
        }, {
            name: 'A101会议室',
            dateText: '2017.5.17-5.19',
        }];
    },

    components: {
        Tab,
        TabItem,
        Sticky,
        Divider,
        XButton,
        Swiper,
        SwiperItem,
        Hecha,
        Huichang,
        Zhusu,
        Laifang,
    },
    methods: {
        jumpTo(componentName) {
            this.$emit('changeComponent', componentName);
        },
        jumpToMeeting(obj) {
            // this.jumpTo('meeting');
        },
        onItemClick(componentName) {
            this.showPage = componentName;
        },
    },
}

</script>

<style lang="scss" scoped>
@import '../../style/mixin';

.container {
    background-color: white;
    height: 100vh;
    @include fj(flex-start, column, center);
    z-index: 1;
}


.header_view {
    background-color: $mainBlue;
    @include fj;
    flex: 0 0 1.44rem;
    height: 1.44rem;
    width: 100%;
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

.tab {
    width: 100%;
}

.body_view {
    @include fj(flex-start, column);
    flex: 1;
    width: 100%;
    margin-top: 0.3rem;

    .item_view {}
}
</style>
