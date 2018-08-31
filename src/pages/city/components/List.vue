<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title borde-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">北京</div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title borde-topbottom">热门城市</div>
                <div class="button-list">
                    <div class="button-wrapper" v-for="item of hot" :key="item.id">
                        <div class="button">{{item.name}}</div>
                    </div>
                </div>
            </div>
            <div class="area" v-for="(item,key) of cities" :key="key">
                <div class="title borde-topbottom">{{key}}</div>
                <div class="item-list">
                    <div class="item border-bottom" v-for="it of item" :key="it.id">{{it.name}}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
    name: 'CityList',
    props:{
        hot:Array,
        cities:Object
    },
    mounted () {
        this.scroll=new Bscroll(this.$refs.wrapper)
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
    .borde-topbottom
        &:before
            border-color: #cccccc
        &:after
            border-color: #cccccc
    .border-bottom
        &:before
            border-color: #cccccc
    .list
        position:absolute
        top:1.58rem
        left:0
        right:0
        bottom:0
        overflow:hidden
        .title
            line-height: .54rem
            background: #eee
            padding-left: .2rem
            color: #666666
            font-size: .26rem
        .button-list
            padding:.1rem .6rem .1rem .1rem
            overflow:hidden
            .button-wrapper
                float:left
                width:33.33%
                .button
                    margin: .1rem
                    padding: .1rem 0
                    text-align: center
                    border: .02rem solid #ccc
                    border-radius: .06rem
        .item-list
            .item
                line-height:.76rem
                padding-left:.2rem
                color: #666666

</style>
