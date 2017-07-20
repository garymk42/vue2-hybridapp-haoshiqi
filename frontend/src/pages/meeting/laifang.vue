<template>
    <div class="container">
        <div style="width:100%" v-for="item,index in list" @click="onClick(item)">
            <div class="item">
                <img v-show="index%3==0" src="../../assets/icon_renyuan1@3x.png"></img>
                <img v-show="index%3==1" src="../../assets/icon_renyuan2@3x.png"></img>
                <img v-show="index%3==2" src="../../assets/icon_renyuan3@3x.png"></img>
                <p>{{item.name}}</p>
                <img class="arrow" v-show="!item.checked" src="../../assets/icon_arrow_shang@3x.png"></img>
                <img class="arrow" v-show="item.checked" src="../../assets/icon_arrow_xia@3x.png"></img>
            </div>
            <div class="container2" v-show="!item.checked">
                <section class="item2" v-for="element,index in item.people" @click="onClick(element)">
                    <p>{{element.name}}</p>
                    <p>{{element.title}}</p>
                    <img  src="../../assets/button_arrow@3x.png"></img>
                </section>
            </div>
        </div>
    
    </div>
     
</template>

<script>  

export default {
    data() {
        return {
            list: [],
        }
    },

    mounted() {
        this.list = [{
            name: '粮食局',
            checked: false,
            people: [{
                name: '王晓明',
                title: '办公室主任',
            }, {
                name: '张三',
                title: '办公室副主任',
            }, {
                name: '丽丽',
                title: '研发部主管',
            },],
        }, {
            name: '创意责任有限公司',
            checked: false,
            people: [{
                name: '王晓明',
                title: '办公室主任',
            }, {
                name: '张三',
                title: '办公室副主任',
            }, {
                name: '丽丽',
                title: '研发部主管',
            },],
        }, {
            name: '文化局',
            checked: false,
            people: [{
                name: '王晓明',
                title: '办公室主任',
            }, {
                name: '张三',
                title: '办公室副主任',
            }, {
                name: '丽丽',
                title: '研发部主管',
            },],
        },];
    },

    components: {

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
        onClick(obj) {
            let arr = [];
            this.list.forEach((item) => {
                if (item.name == obj.name)
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
.container {
    @include fj(flex-start, column);
    margin-top: 0.24rem;

    width: 100%;
    .item {
        @include fj(flex-start, row);
        background: url(../../assets/button_bg@3x.png) no-repeat;
        min-height: 1.41rem;
        font-size: 0.48rem;
        width: 95%;
        box-shadow: 2px 2px 2px #e0e0e0;
        margin-left: 0.24rem;
        margin-right: 0.24rem;
        margin-bottom: 0.24rem;
        p {
            flex: 1;
        }
        img {
            margin-left: 0.56rem;
            margin-right: 0.3rem;
            height: 1rem;
            width: 1rem;
        }
        .arrow {
            height: 0.3rem;
            width: 0.5rem;
        }
        .checked {
            text-decoration: line-through;
            color: #90949d;
        }
        .unchecked {
            color: #585d6a;
            text-decoration: none;
        }
    }
}

.container2 {
    @include fj(flex-start, column);
    margin-top: 0.24rem;
    margin-left:5%;
    width: 90%;
    .item2 {
        @include fj(flex-start, row);
        background: url(../../assets/button_bg@3x.png) no-repeat;
        min-height: 1.41rem;
        font-size: 0.48rem;
        width: 95%;
        box-shadow: 2px 2px 2px #e0e0e0;
        margin-left: 0.24rem;
        margin-right: 0.24rem;
        margin-bottom: 0.24rem;
        p:first-child {
            margin-left: 1rem;
            width:3rem;
        }
        img {
            margin-left: 0.56rem;
            margin-right: 0.3rem;
            height: 1rem;
            width: 1rem;
        }
    }
}
</style>
