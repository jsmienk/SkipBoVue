<template>
    <div class="card-stock">
        <playing-card
            v-for="(card, i) in cards"
            :key="card.id"
            :rank="card.rank"
            :isFaceUp="card.isFaceUp"
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
            default: []
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
.card-stock {
    margin: 16px;
    padding: 16px;
    border-radius: 10px;
    height: 260px;
    position: relative;

    .playing-card {
        left: 0;
        transition: left 100ms ease;

        &:hover {
            left: -34px;
        }
    }
}
</style>
