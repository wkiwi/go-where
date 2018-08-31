<template>
    <div class="header">
        城市选择
        <router-link to="/">
            <div class="iconfont header-back">&#xe624;</div>
        </router-link>
    </div>
</template>

<script>
export default {
    name: 'CityHeader'
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
    .header
        position:relative
        overflow: hidden
        height:$headerHeight
        line-height:$headerHeight
        text-align :center
        color:#fff
        background: $bgColor
        font-size:.32rem
        .header-back
            font size 0.4rem
            position:absolute
            top:0
            left:0
            height: 0.86rem
            line-height:.86rem
            text-align:center
            color:#fff
            width:.64rem
</style>
