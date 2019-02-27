<template>
  <div class="card-stack" :class="{small: !isUser && !isTower}">
    <playing-card
      v-for="(card, i) in cards"
      :key="card.id"
      :rank="card.rank"
      :isFaceUp="card.isFaceUp"
      :isSmall="!isUser && !isTower"
      :class="{selectable: isUser && i == cards.length - 1}"
      :style="getCardStyle(i)"
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
    isUser: {
      type: Boolean,
      default: false
    },
    isTower: {
      type: Boolean,
      default: false
    },
    rotate: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      rotationOffset: shuffle([-10, -5, 0, 5, 10])
    };
  },
  methods: {
    getCardStyle(index) {
      return `
                transform: rotate(${
                  this.rotate
                    ? this.rotationOffset[
                        (index * 2) % this.rotationOffset.length
                      ]
                    : 0
                }deg);
            `;
    }
  }
};

// LOCAL HELPER
function shuffle(a) {
  let i = a.length,
    t,
    r;
  while (0 !== i) {
    r = Math.floor(Math.random() * i);
    i -= 1;
    t = a[i];
    a[i] = a[r];
    a[r] = t;
  }
  return a;
}
</script>

<style lang="scss">
@import "./../style/vars.scss";

.card-stack {
  margin: $m-normal;
  border-radius: $card-radius;
  width: $card-width;
  height: $card-height;
  position: relative;
  display: inline-block;
  border: $card-placeholder-border;

  &.small {
    margin: $m-tiny;
    width: $card-small-width;
    height: $card-small-height;
    border-radius: $card-small-radius;
  }

  .playing-card {
    top: 0;

    &.selectable {
      transition: $card-hover-transition;

      &:hover {
        top: $card-hover-top;
      }
    }
  }
}
</style>
