<template>
  <div class="player-area" :class="{'is-enemy': !isUser, 'is-turn': isTurn}">
    <h3 class="player-name">{{ player.name }}</h3>
    <Stock
      v-for="(stock, i) in player.stocks"
      :key="i"
      :cards="stock"
      :isUser="isUser"
      class="player-area-stock"
    />
    <Stack
      :cards="player.stack"
      :rotate="false"
      :isUser="isUser"
      class="player-area-stack"
    />
    <Hand :cards="player.stocks[1]" :isUser="isUser" class="player-area-hand"/>
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
    isUser: {
      type: Boolean,
      default: false
    },
    isTurn: {
      type: Boolean,
      default: false
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
        DUMMY_CARD(),
        DUMMY_CARD()
      ],
      [
        DUMMY_CARD(),
        DUMMY_CARD(),
        DUMMY_CARD(),
        DUMMY_CARD()
      ],
      [],
      [
        DUMMY_CARD()
      ]
    ],
    stack: [
      DUMMY_CARD()
    ],
    hand: []
  };
}

function DUMMY_CARD() {
  return {
    id: Math.floor(Math.random() * 1000),
    rank: Math.floor(Math.random() * 13),
    isFaceUp: true
  };
}
</script>

<style lang="scss">
@import "./../style/vars.scss";

.player-area {
  width: 1100px;
  margin: 0 auto;
  border-radius: $card-radius;

  .player-name {
    margin: 0 18px 0 18px;
    padding: $m-tiny;
  }

  &.is-turn .player-name {
    color: $color-card-selected-border;
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
    padding: $m-tiny $m-tiny 0 $m-tiny;
    width: 362px;
    display: inline-block;
    transform: rotate(180);

    &.is-turn {
      border: $player-area-turn-border;
      box-shadow: $player-area-turn-glow;
    }

    .player-name {
      margin: 0 $m-small 0 $m-small;
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
