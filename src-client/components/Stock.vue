<template>
  <div class="card-stock" :class="{small: !isPlayersHand}">
    <playing-card
      v-for="(card, i) in cards"
      :key="card.id"
      :rank="card.rank"
      :isFaceUp="card.isFaceUp"
      :isSmall="!isPlayersHand"
      :style="getCardStyle(i)"
      :class="{
                'no-focus': cards.length > numberOfCardsFocus && i < cards.length - numberOfCardsFocus,
                'selectable': i == cards.length - 1 && isPlayersHand
            }"
    />
  </div>
</template>

<script>
import PlayingCard from "./PlayingCard.vue";

export default {
  components: {
    PlayingCard
  },
  props: {
    cards: {
      type: Array,
      default: function() {
        return [];
      }
    },
    isPlayersHand: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      overlapOffsetMin: 6,
      numberOfCardsFocus: 3
    };
  },
  computed: {
      overlapOffset() { return this.isPlayersHand ? 32 : 20; },
  },
  methods: {
    getCardStyle(index) {
      const nr = this.cards.length;
      let offset = 0;
      // More cards than can be in focus
      if (nr > this.numberOfCardsFocus) {
        const threshold = nr - this.numberOfCardsFocus;
        // This card is out of focus
        if (index < threshold) {
          offset = index * this.overlapOffsetMin;
        } else {
          // This card is in focus
          offset =
            (index - threshold) * this.overlapOffset +
            threshold * this.overlapOffsetMin;
        }
      } else {
        // All cards in focus
        offset = index * this.overlapOffset;
      }

      return `top: ${offset}px;`;
    }
  }
};
</script>

<style lang="scss">
@import "./../style/vars.scss";

.card-stock {
  margin: $m-normal;
  margin-bottom: $stock-margin-bottom;
  border-radius: $card-radius;
  width: $card-width;
  height: $card-height;
  display: inline-block;
  position: relative;
  border: $card-placeholder-border;

  &.small {
    margin-bottom: $stock-small-margin-bottom;
    width: $card-small-width;
    height: $card-small-height;
    border-radius: $card-small-radius;
  }

  .playing-card {
    left: 0;
    transition: $card-hover-transition;

    &.no-focus:hover {
      left: $card-hover-left;

      &.small {
          left: $card-small-hover-left;
      }
    }
  }
}
</style>
