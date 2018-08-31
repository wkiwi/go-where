<template>
    <div>
        <div class="search">
            <input v-model="keyword" class="search-input" type="text" placeholder="输入城市或拼音">
        </div>
        <div class="search-content" ref="search" v-show="keyword">
            <ul>
                <li class="search-item border-bottom" v-for="item of list" :key="item.id">{{item.name}}</li>
                <li class="search-item border-bottom" v-show="hasNoData">没有找到数据</li>
            </ul>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
    name: 'CitySearch',
    props:{
        cities:Object
    },
    data () {
        return{
            keyword:"",
            list:[],
            timer:null
        }
    },
    computed:{
       hasNoData(){
           return !this.list.length
       } 
    },
    mounted () {
        this.scroll=new Bscroll(this.$refs.search)
    },
    watch:{
        keyword () {
            if(this.timer){
                clearTimeout(this.timer)
            }
            if(!this.keyword){
                this.list=[]
                return
            }
            this.timer=setTimeout(()=>{
                const result=[]
                for (let i in this.cities){
                    this.cities[i].forEach((value)=>{
                        if (value.spell.indexOf(this.keyword)>-1 || value.name.indexOf(this.keyword)>-1){
                            result.push(value)
                        }
                    })
                }
                this.list=result
            },100)
        }
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
    .search
        height:.72rem
        background:$bgColor
        padding:0 .1rem
        .search-input
            box-sizing:border-box
            height:.62rem
            line-height:.62rem
            width:100%
            padding:0 .1rem
            border-radius:.06rem
            text-align:center
            color:#666
    .search-content
        position:absolute
        top:1.58rem
        left:0
        right 0
        bottom:0
        z-index:1
        background:#eee
        overflow:hidden
        .search-item
            line-height:.62rem
            padding-left: .2rem
            color: #666
            background:#fff




</style>
