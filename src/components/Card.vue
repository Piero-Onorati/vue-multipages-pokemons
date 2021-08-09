<template>
    <div  class="card">

        <!-- CARD IMG -->
        <div class="card-img">
            <img :src="details.images['small']" :alt="details.name">
        </div>

        <!-- CARD INFO -->
        <div class="info-card">
            <!-- NAME -->
            <h3 class="card-name">{{details.name}}</h3>
            <!-- RARITY -->
            <h4 class="card-rarity">{{details.rarity}}</h4>
            <!-- TYPE -->
            <span class="type" v-for="(item,index) in details.types" :key="'e'+ index" :class="item.toUpperCase()">{{item.toUpperCase()}}</span>
            <!-- SUPERTYPE -->
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

        .card-name{
            color: black;;
        }

        .card-rarity{
            color: #3e3e3e;
            font-size: 14px;
            padding: 3px 0 10px 0;
        }

        .type{
            font-size:14px;
            border-radius:5px;
            padding: 0px 6px;
            margin: 0 5px;
        }
    
        .supertype{
            font-size: 14px;
            font-style: italic;
            color: dimgrey;
            padding-top: 5px;
        }
    }

}

</style>