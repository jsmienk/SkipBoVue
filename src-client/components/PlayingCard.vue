<template>
  <div class="playing-card" :class="{small: isSmall}" :style="style">
    <div v-if="isFaceUp">
      <div class="top-rank" :class="{small: isSmall}">{{ rankString }}</div>
      <div>{{ rankMainString }}</div>
      <div class="bottom-rank" :class="{small: isSmall}">{{ rankString }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    rank: {
      type: Number,
      default: 10
    },
    isFaceUp: {
      type: Boolean,
      default: true
    },
    isSmall: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      rankClasses: [
        {
          range: [0],
          color: "#ffa343"
        },
        {
          range: [1, 2, 3, 4],
          color: "#437cff"
        },
        {
          range: [5, 6, 7, 8],
          color: "#3aac30"
        },
        {
          range: [9, 10, 11, 12],
          color: "#c52b42"
        }
      ],
      faceDownColor: "#555",
      jokerRankName: ["skip", "bo"]
    };
  },
  computed: {
    rankClass() {
      for (const c of this.rankClasses) {
        if (c.range.includes(this.rank)) return c;
      }
    },
    rankMainString() {
      return this.isFaceUp
        ? this.rank === 0
          ? this.jokerRankName[1]
          : this.rank
        : "";
    },
    rankString() {
      return this.isFaceUp
        ? this.rank === 0
          ? this.jokerRankName[0]
          : this.rank
        : "";
    },
    style() {
      return `
                background-color: ${
                  this.isFaceUp ? this.rankClass.color : this.faceDownColor
                };
            `;
    }
  }
};
</script>

<style lang="scss">
@import "./../style/vars.scss";

.playing-card {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;

  font-weight: bold;
  font-size: $card-font-size;
  text-align: center;
  text-transform: uppercase;
  color: $color-card-border;

  position: absolute;
  width: $card-width;
  height: $card-height;
  padding: $card-padding;
  border-radius: $card-radius;
  border: $card-border $color-card-border;

  &.selectable {
    &:hover {
      border: $card-border $color-card-selected-border;
      box-shadow: $color-card-selected-glow;

      &.small {
        border: $card-small-border $color-card-selected-border;
      }
    }
  }

  &.small {
    font-size: $card-small-font-size;
    width: $card-small-width;
    height: $card-small-height;
    padding: $card-small-padding;
    border-radius: $card-small-radius;
    border: $card-small-border $color-card-border;
  }

  .top-rank,
  .bottom-rank {
    font-size: $card-mark-font-size;
    text-align: left;
    text-transform: capitalize;

    &.small {
      font-size: $card-small-mark-font-size;
    }
  }

  .top-rank {
    margin-bottom: $card-rank-margin;

    &.small {
      margin-bottom: $card-small-rank-margin;
    }
  }

  .bottom-rank {
    transform: rotate(180deg);
    margin-top: $card-rank-margin;

    &.small {
      margin-top: $card-small-rank-margin;
    }
  }
}
</style>
