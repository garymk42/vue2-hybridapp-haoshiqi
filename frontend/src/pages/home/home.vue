<template>
<div>
  
    <div class="container">
        <div class="header_view">
            <div class="side_btn" @click="showSide=true"></div>
            <p>首页</p>
            <div class="notice_btn" @click="jumpTo('notices')"></div>
        </div>
        <div class="calendar_view">
            <div class="bar">
                <span class="deduct" @click="deduct">
                    <i class="arrow-left"></i>
                </span>{{selectMonth.year}}年 {{selectMonth.month}}月
                <span class="add" @click="add">
                    <i class="arrow-right"></i>
                </span>
            </div>
            <div class="calendar_container">
                <div class="calendar_item big" v-for="index of 7">
                    {{getBigText(index)}}
                </div>
            </div>
            <div class="calendar_container">
                <div v-for="day of dateArr" :class="{'calendar_item small':true,
                        'black' : day.isCurMonth,
                        'type1 typo-em':day.isType1,
                        'type2 typo-em':day.isType2,
                        'type3 typo-em':day.isType3,
                        'today' : day.isToday}" @click="clickItem(day.date)">
                    <section :class="{'calendar_item_in':true,
                            'checked':day.isChecked,
                            'today' : day.isToday}">
                        <p>{{day.day}}</p>
                    </section>
                </div>
            </div>
        </div>
        <div class="list_view">
            <div class="list_item" v-for="meeting,index in meetings">
                <div class="left">
                    <img v-if="index%3 == 0" src="../../assets/huiyi_dian1@3x.png"></img>
                    <img v-if="index%3 == 1" src="../../assets/huiyi_dian2@3x.png"></img>
                    <img v-if="index%3 == 2" src="../../assets/huiyi_dian3@3x.png"></img>
                </div>
                <div class="middle"  @click="jumpTo('meeting')">
                    <div class="r1">
                        <p class="p1">{{meeting.name}}</p>
                        <p class="p2">{{meeting.timeText}}</p>
                    </div>
                    <div class="r2">
                        <p>{{meeting.statusText}}</p>
                    </div>
                </div>
                <div class="right" @click="jumpTo('meeting')">
                    <img src="../../assets/button_arrow@3x.png"></img>
                </div>
            </div>
            <div class="end">
                已是页面底部
            </div>
            <div class="footer">
                没有更多内容了
            </div>
        </div>
    </div>
    <div class="side_view" v-show="showSide" v-if="!showLogin && !showNotice">
        <section class="side_a">
            <section class="side_name"><img src="../../assets/icon_xingming@3x.png"></img>张晓溪</section>
            <section class="side_logout" @click="jumpTo('login')">
                <img src="../../assets/icon_zhuxiao@3x.png"></img>
                注销
                <img src="../../assets/button_arrow@3x.png"></img>
            </section>
        </section>
        <section class="side_b" @click="showSide=false"></section>
    </div>
</div>
</template>

<script> 
import moment from 'moment'
import Login from '../login/login'
import Notices from '../notices/notices'
export default {
    data() {
        return {
            showLogin:false,
            showNotice:false,
            showSide:false,
            username: "",
            password: "",
            dateArr: [],
            selectMonth: {
                year: "",
                month: "",
            },
            allMeetings: [],
            meetings: [],
        }
    },

    mounted() {
        const now = moment();
        this.selectMonth.year = now.format('YYYY');
        this.selectMonth.month = now.format('MM');
        this.renderCal(this.selectMonth);
        this.allMeetings = [{
            name: '公司章程会议',
            timeText: '2017.6.17-6.19',
            startDay: '2017-6-17',
            endDay:'2017-6-19',
            statusText: '预定会场',
        }, {
            name: '运营部署会议',
            timeText: '2017.6.17-6.18',
            startDay: '2017-6-17',
            endDay:'2017-6-18',
            statusText: '预定用车',
        }, {
            name: '项目运营部署会议',
            timeText: '2017.6.17',
            startDay: '2017-6-17',
            endDay:'2017-6-17',
            statusText: '预定会场',
        }, {
            name: '公司章程会议',
            timeText: '2017.6.17-6.19',
            startDay: '2017-6-17',
            endDay:'2017-6-19',
            statusText: '预定会场',
        },];

        this.clickItem(moment().format('YYYY-MM-DD'));
    },

    components: {
        Login,
        Notices,
    },
    //:class="{'today' : day.isToday,
    //   'not-cur-month' : !day.isCurMonth}"
    methods: {
        renderCal(obj) {
            const arr1 = ['2017-06-05', '2017-06-10', '2017-06-11'];
            const arr2 = ['2017-06-17', '2017-06-18'];
            const arr3 = ['2017-06-19'];
            let tempArr = [];

            const firstOfMonth = moment(obj.year + '-' + obj.month + '-01', 'YYYY-MM-DD');
            let tempDay = firstOfMonth.startOf('week');
            for (let i = 0; i < 35; i++) {
                tempDay = tempDay.add(1, 'days');
                let day = {};
                day.isToday = tempDay.format('YYYY-MM-DD') == moment().format('YYYY-MM-DD');
                day.date = tempDay.format('YYYY-MM-DD');
                day.day = tempDay.format('D');
                day.isCurMonth = tempDay.format('MM') == obj.month;
                day.isType1 = arr1.indexOf(tempDay.format('YYYY-MM-DD')) != -1;
                day.isType2 = arr2.indexOf(tempDay.format('YYYY-MM-DD')) != -1;
                day.isType3 = arr3.indexOf(tempDay.format('YYYY-MM-DD')) != -1;
                day.isChecked = false;
                tempArr.push(day);
            }
            this.dateArr = tempArr;
        },
        clickItem(date) {
            let arr = [];
            this.dateArr.forEach((item, index) => {
                item.isChecked = item.date == date;
                arr.push[item];
            });
            this.dataArr = [...arr];

            arr = [];
            this.allMeetings.forEach((item)=>{
                console.log('item.startDay',item.startDay);
                console.log('item.endDay',item.endDay);
                console.log('date',date);
                console.log('moment(item.startDay).isBefore(date)',moment(item.startDay).isBefore(date));
                console.log(' moment(item.endDay).isAfter(date)', moment(item.endDay).isAfter(date));

                if( (moment(item.startDay).isBefore(date)|| moment(item.startDay).isSame(date) )
                 && (moment(item.endDay).isAfter(date) || moment(item.endDay).isSame(date) ) ){
                    arr.push(item);
                }
            });
            this.meetings = arr;
        },
        jumpTo(componentName){
            this.$emit('changeComponent',componentName);
        },
        add() {
            const day = moment(this.selectMonth.year + '-' + this.selectMonth.month + '-01', 'YYYY-MM-DD');
            day.add(1, 'month');
            this.selectMonth.year = day.format('YYYY');
            this.selectMonth.month = day.format('MM');
            this.renderCal(this.selectMonth);
        },
        deduct() {
            const day = moment(this.selectMonth.year + '-' + this.selectMonth.month + '-01', 'YYYY-MM-DD');
            day.add(-1, 'month');
            this.selectMonth.year = day.format('YYYY');
            this.selectMonth.month = day.format('MM');
            this.renderCal(this.selectMonth);
        },
        getBigText(index) {
            const bigArr = ['', '一', '二', '三', '四', '五', '六', '日',];
            return bigArr[index];
        },
    },
}

</script>

<style lang="scss" scoped>
@import '../../style/mixin';
.container {
    background-color: $mainBlue;
    height: 100vh;
    @include fj(flex-start,column,center);
    z-index:1;
}

.header_view {
    @include fj;
    flex: 0 0 1.44rem;
    height: 1.44rem;
    width: 10.4rem;
    p {
        @include sc(0.54rem, white);
    }
    .side_btn {
        margin-left: 0.12rem;
        background: url(../../assets/button_cebianlan@3x.png) no-repeat 0 0;
        background-size: cover;
        height: 0.52rem;
        width: 0.6rem;
    }
    .notice_btn {
        margin-right: 0.12rem;
        background: url(../../assets/button_xiaoxi@3x.png) no-repeat 0 0;
        background-size: cover;
        height: 0.52rem;
        width: 0.46rem;
    }
}

.calendar_view {
    flex: 0 0 9.95rem;
    background: url(../../assets/bg_rili@3x.png) no-repeat;
    background-size: contain;
    width: 10.4rem;
    height: 9.95rem;
    .bar {
        height: 1.52rem;
        border-bottom: 1px solid $lineGrey;
        margin-bottom: 0.14rem;
        @include fj(center,row,center);
        @include sc(0.48rem, #90949d);
        .arrow-left{
            background: url(../../assets/left-arrow.svg) no-repeat;
            background-size: contain;
            width: 0.25rem;
            height: 0.25rem;
        }
        .arrow-right{
            background: url(../../assets/right-arrow.svg) no-repeat;
            background-size: contain;
            width: 0.25rem;
            height: 0.25rem;
        }
        .deduct {
            @include fj;
            justify-content: center;
            width: 1rem;
            height: 1rem;
        }
        .add {
            @include fj;
            justify-content: center;
            width: 1rem;
            height: 1rem;
        }
    }
    .calendar_container {
        @include fj(flex-start,row,center);
        flex-wrap: wrap;
        margin-left: 0.30rem;
        width: 9.8rem;
        .calendar_item {
            flex: 0 0 1.37rem; // width:1.44rem;
            width: 1.37rem;
            height: 1.17rem;
            line-height: 1.3rem;
            @include fj(center,row,center);
            &.big {
                @include sc(0.52rem, #cccccc);
            }
            &.small {
                @include sc(0.48rem, #cccccc);
            }
            &.black {
                color: black;
            }
            &.today {
                // background-color:#00acfa;
                // border-radius: 50%;
                // padding-left:0.1rem;
            }
            &.type1 {
                color: #fb9f65;
            }
            &.type2 {
                color: #00acfa;
            }
            &.type3 {
                color: #7ed321;
            }
        }
        .calendar_item_in {
            width: 1rem;
            height: 1rem;
            border-radius: 50%;
            line-height: 1rem;
            text-align: center;
            &.today {
                background-color: #00acfa;
                color: white;
            }
            &.checked {
                border: 1px solid #00acfa;
            }
        }
    }
}

.typo-em {
    position: relative;
}

.typo-em:after {
    position: absolute;
    bottom: 0.1rem;
    left: 0;
    width: 100%;
    overflow: hidden;
    white-space: nowrap;
    text-align: center;
    content: ".";
}



/* Responsive images */

.typo img {
    max-width: 100%;
}

.list_view {
    overflow: auto;
    width: 100%;
    @include fj(space-between,column,center);
    .list_item {
        flex:0 0 auto;
        width:100%;
        @include fj;
        .left {
            @include fj(center,row,center);
            flex: 0 0 1.5rem;
            height: 2.47rem;
            img {
                width: 0.3rem;
                height: 0.3rem;
            }
        }
        .middle {
            flex: 1 0 7rem;
            height: 2.47rem;
            @include fj(center,column,center);
            flex-direction: column;
            justify-content: center;
            border-bottom: 1px solid $lineGrey;
            .r1 {
                width: 100%;
                @include fj;
                .p1 {
                    @include sc(0.48rem, white);
                    margin-bottom: 0.15rem;
                }
                .p2 {
                    @include sc(0.36rem, #90949d);
                }
            }
            .r2 {
                width: 100%;
                p {
                    @include sc(0.42rem, #90949d);
                }
            }
        }
        .right {
            @include fj(center,row,center);
            flex: 0 0 1.5rem;
            height: 2.47rem;
            border-bottom: 1px solid $lineGrey;
            img {
                width: 0.3rem;
            }
        }
    }
    .end{
        margin-top:1.19rem;
        margin-bottom:0.41rem;
        padding-top:0.2rem;
        width:2.38rem;
        height:1.54rem;
        flex:0 0 1.54rem;
        background: url('../../assets/icon_dibu@3x.png') no-repeat;
        background-size: contain;
        text-align:center;
        font-size:0.32rem;
        color:#aebec8;
    }
    .footer{
        font-size:0.36rem;
        color:#aebec8; 
        margin-bottom:1.03rem; 
    }
}
.side_view{
    position:fixed;
    top:0px;
    height:100vh;
    width:100%;
    z-index:99;
    @include fj(flex-start,row);
    .side_a{
        flex:0 0 4.23rem;
        height:100%;
        width:100%;
        background-color:$mainBlue;
        @include fj(flex-start,column);
        .side_name{
            @include fj(flex-start,row);
            @include sc(0.54rem,white);
            flex:0 0 1.81rem;
            margin-right:0.3rem;
            img{
                margin-right:0.5rem;
                height:0.5rem;
                width:0.5rem;
            }
        }
        .side_logout{
            @include fj(flex-start,row);
            @include sc(0.54rem,white);
            flex:0 0 1.81rem;
            img{
                margin-right:0.3rem;
                height:0.5rem;
                width:0.5rem;
            }
            img:last-child{
                margin-left:0.2rem;
                height:0.5rem;
                width:0.3rem;
            }
        }
    }
    .side_b{
        flex:1;
        height:100vh;
        width:100%;
        background-color:grey;
        opacity: 0.4;
    }
}
</style>
