<template>
    <div  class="card">
        <img :src="details.images['small']" :alt="details.name">
        <h3>{{details.name}}</h3>
        <h4>{{details.rarity}}</h4>
        <span class="type" v-for="(item,index) in details.types" :key="'e'+ index" :class="item.toUpperCase()">{{item.toUpperCase()}}</span>
        <h4 class="supertype">{{details.supertype}}</h4>
    </div>
</template>

<script>
export default {
    name:'Card',
    props:{
        details:Object
    }

}
</script>

<style lang="scss" scoped>
.card{
    position: relative;
    width: calc((100% / 4) - 30px);
    margin:15px;

    img{
        width:100%
    }
    
    &:after {
        content: "";
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        top: 0;
        background-repeat: no-repeat;
        opacity: .5;
        mix-blend-mode: color-dodge;
        transition: all .33s ease;
    }
    
    &:after {
        opacity: 1;
        background-image: url("https://assets.codepen.io/13471/sparkles.gif"), 
        url(https://assets.codepen.io/13471/holo.png), 
        linear-gradient(125deg, #ff008450 15%, #fca40040 30%, #ffff0030 40%, #00ff8a20 60%, #00cfff40 70%, #cc4cfa50 85%);
        background-position: 50% 50%;
        background-size: 160%;
        background-blend-mode: overlay;
        z-index: 2;
        filter: brightness(1) contrast(1);
        transition: all .33s ease;
        mix-blend-mode: color-dodge;
        opacity: .75;
    }

    &:hover:after {
        filter: brightness(1) contrast(1);
        opacity: 1;
    }

    .type{
        font-size:14px;
        border-radius:5px;
        padding: 0px 6px;
        margin-right: 10px;

    }

    .supertype{
        font-size: 16px;
        font-style: italic;
    }

}

</style>