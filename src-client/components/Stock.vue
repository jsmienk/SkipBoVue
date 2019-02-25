<template>
    <div class="card-stock">
        <playing-card
            v-for="(card, i) in cards"
            :key="card.id"
            :rank="card.rank"
            :isFaceUp="card.isFaceUp"
            :style="getCardStyle(i)"
            :class="{'no-focus': cards.length > numberOfCardsFocus && i < cards.length - numberOfCardsFocus}"
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
            default: function() { return [] }
        },
        isPlayerHand: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            overlapOffset: 32,
            overlapOffsetMin: 6,
            numberOfCardsFocus: 3
        }
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
                    offset = (index - threshold) * this.overlapOffset + threshold * this.overlapOffsetMin;
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
    border-radius: $card-radius;
    width: $card-width;
    height: $stock-height;
    display: inline-block;
    position: relative;
    border: $card-placeholder-border;

    .playing-card {
        left: 0;
        transition: $card-hover-transition;

        &.no-focus:hover {
            left: $card-hover-left;
        }
    }
}
</style>
