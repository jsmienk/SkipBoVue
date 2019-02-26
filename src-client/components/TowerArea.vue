<template>
  <div class="tower-area">
    <Stack
      v-for="(tower, i) in this.towers"
      :key="i"
      :cards="tower"
      :rotate="true"
      :isTower="true"
      class="tower"
    />
    <Stack :cards="stack" :rotate="false" :isTower="true" class="pile"/>
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
    towers: {
      type: Array,
      default: function() {
        return [
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
        ];
      }
    },
    stack: {
      type: Array,
      default: function() {
        return [];
      }
    }
  },
  data() {
    return {};
  }
};
</script>

<style lang="scss">
@import "./../style/vars.scss";

.tower-area {
  width: 760px;
  margin: 32px auto 16px;

  .tower {
    margin-right: 10px;
  }

  .pile {
    margin-left: 80px;
    vertical-align: top;
  }
}
</style>
