<template>
    <div  class="card">
        <div class="card-img">
            <img :src="details.images['small']" :alt="details.name">
        </div>
        <div class="info-card">
            <h3>{{details.name}}</h3>
            <h4>{{details.rarity}}</h4>
            <span class="type" v-for="(item,index) in details.types" :key="'e'+ index" :class="item.toUpperCase()">{{item.toUpperCase()}}</span>
            <h4 class="supertype">{{details.supertype}}</h4>
        </div>
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
    border-radius:10px;
    cursor: pointer;

    .card-img{
        width:100%;
        height: 280px;
        border-radius:10px;
        overflow: hidden;

        img{
            width:100%;
            height:100%
        }

    }

        
    &:hover .card-img{
        transform: scale(1.03);
        box-shadow: 0 4px 10px rgba(0,0,0,0.15), 0 10px 10px rgba(0,0,0,0.12)
    }

    .info-card{
        text-align: center;
        padding-top:20px;

        .type{
            font-size:14px;
            border-radius:5px;
            padding: 0px 6px;
            margin: 0 5px;
        }
    
        .supertype{
            font-size: 16px;
            font-style: italic;
        }
    }


  

    


}

</style>