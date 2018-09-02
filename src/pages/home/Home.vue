<template>
    <div>
        <home-header></home-header>
        <home-swiper :list="swiperList"></home-swiper>
        <home-icons :list="iconList"></home-icons>
        <home-recommend :list="recommendList"></home-recommend>
        <home-weekend :list="weekendList"></home-weekend>
    </div>
</template>s

<script>
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import axios from 'axios'
import { mapState } from 'vuex'
export default {
    name: 'Home',
    data () {
        return {
            lastCity:"",
            swiperList:[],
            iconList:[],
            recommendList:[],
            weekendList:[]
        }
    },
    computed:{
        ...mapState(["city"])
    },
    components: {
        HomeHeader,
        HomeSwiper,
        HomeIcons,
        HomeRecommend,
        HomeWeekend
    },
    mounted () {
        this.getHomeInfo()
        this.lastCity=this.city
    },
    methods:{
        getHomeInfo:function(){
            axios.get('/api/index.json?city='+this.city)
                .then(this.getHomeInfoSucc)
        },
        getHomeInfoSucc:function(res){
            res=res.data
            if(res.ret && res.data){
                const data=res.data
                this.swiperList=data.swiperList
                this.iconList=data.iconList
                this.recommendList=data.recommendList
                this.weekendList=data.weekendList
            }
        }
    },
    activated (){
        console.log(this.lastCity)
        console.log(this.city)
        if(this.lastCity !== this.city){
            this.lastCity=this.city
            this.getHomeInfo()
        }
    }
}
</script>

<style lang="stylus" scoped>
    
</style>
