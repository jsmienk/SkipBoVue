<template>
  <div class="player-area" :class="{'is-enemy': !isPlayersArea}">
    <h3 class="player-name">{{ player.name }}</h3>
    <Stock
      v-for="(stock, i) in player.stocks"
      :key="i"
      :cards="stock"
      :isPlayersHand="isPlayersArea"
      class="player-area-stock"
    />
    <Stack
      :cards="player.stack"
      :rotate="false"
      :isPlayersHand="isPlayersArea"
      class="player-area-stack"
    />
    <Hand :cards="player.stocks[1]" :isPlayersHand="isPlayersArea" class="player-area-hand"/>
  </div>
</template>

<script>
import Stack from "./Stack.vue";
import Stock from "./Stock.vue";
import Hand from "./Hand.vue";

export default {
  components: {
    Stack,
    Stock,
    Hand
  },
  props: {
    player: {
      type: Array,
      default: function() {
        return DUMMY_PLAYER();
      }
    },
    isPlayersArea: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {};
  }
};

// DUMMY
function DUMMY_PLAYER() {
  return {
    name: "Player 1",
    stocks: [
      [
        {
          id: 0,
          rank: 2,
          isFaceUp: true
        }
      ],
      [
        {
          id: 0,
          rank: 12,
          isFaceUp: true
        },
        {
          id: 1,
          rank: 2,
          isFaceUp: true
        },
        {
          id: 2,
          rank: 8,
          isFaceUp: true
        },
        {
          id: 3,
          rank: 6,
          isFaceUp: true
        },
        {
          id: 4,
          rank: 9,
          isFaceUp: true
        }
      ],
      [],
      [
        {
          id: 0,
          rank: 11,
          isFaceUp: true
        }
      ]
    ],
    stack: [
      {
        id: 0,
        rank: 8,
        isFaceUp: true
      }
    ],
    hand: []
  };
}
</script>

<style lang="scss">
@import "./../style/vars.scss";

.player-area {
  width: 1100px;
  margin: 0 auto;

  .player-name {
    margin: $m-tiny 0 0 18px;
  }

  .player-area-stock {
    margin-right: 10px;
  }

  .player-area-stack {
    margin-left: 30px;
    vertical-align: top;
  }

  .player-area-hand {
    margin-left: 0;
    vertical-align: top;
  }

  &.is-enemy {
    width: 360px;
    display: inline-block;
    transform: rotate(180);

    .player-name {
    margin: $m-tiny 0 0 $m-small;
  }

    .player-area-stock {
      margin-left: 4px;
      margin-right: 4px;
      z-index: 1;
    }

    .player-area-stack {
      margin-left: 14px;
    }

    .player-area-hand {
      margin-left: 80px;
      z-index: 0;
    }
  }
}
</style>
