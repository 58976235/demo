<template>
    <div class="me-box" :style="{width:widthStr,height:heightStr,left:leftStr,top:topStr}">
    </div>
</template>

<script>
export default {
    props:{
        width:{
            type:Number
        },
        height:{
            type:Number
        },
        top:{
            type:Number
        },
        left:{
            type:Number
        }
    },
    computed:{
        leftStr(){
            return this.left+'px'
        },
        topStr(){
            return this.top+'px'
        },
        widthStr(){
            return this.width+'px'
        },
        heightStr(){
            return this.height+'px'
        }
    }
}
</script>

<style lang="scss" scoped>
.me-box{
    position:absolute;
    z-index: 999;
    background-image: url('../assets/images/me1.png');
}
</style>