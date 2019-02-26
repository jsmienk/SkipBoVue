<template>
    <div class="player-area" :class="{'is-enemy': !isPlayersArea}">
        <Stock 
            v-for="(stock, i) in this.stocks"
            :key="i"
            :cards="stock"
            :isPlayerHand="isPlayersArea"
            class="player-area-stock"
        />
        <Stack 
            :cards="stack" 
            :rotate=false 
            :isPlayerHand="isPlayersArea" 
            class="player-area-stack"
        />
    </div>
</template>

<script>
import Stack from "./Stack.vue";
import Stock from "./Stock.vue";

export default {
    components: {
        Stack,
        Stock
    },
    props: {
        stocks: {
            type: Array,
            default: function() { return [[
                {
                id: 0,
                rank: 2,
                isFaceUp: true
                }
            ], [
                {
                id: 0,
                rank: 12,
                isFaceUp: true
                },{
                id: 1,
                rank: 2,
                isFaceUp: true
                },{
                id: 2,
                rank: 8,
                isFaceUp: true
                },{
                id: 3,
                rank: 6,
                isFaceUp: true
                }
            ], [], [
                {
                id: 0,
                rank: 11,
                isFaceUp: true
                }
            ]]}
        },
        stack: {
            type: Array,
            default: function() { return [{
                id: 0,
                rank: 8,
                isFaceUp: true
                }] }
        },
        isPlayersArea: {
            type: Boolean,
            default: true
        }
    },
    data() {
        return {}
    }
}
</script>

<style lang="scss">
@import "./../style/vars.scss";

.player-area {

    .player-area-stock {
        margin-right: 10px;
    }

    .player-area-stack {
        margin-left: 30px;
        vertical-align: top;
    }
    
    &.is-enemy {
        transform: rotate(180);
    }
}
</style>
