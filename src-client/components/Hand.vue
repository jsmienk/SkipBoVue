<template>
    <div class="card-hand">
        <playing-card
            v-for="(card, i) in cards"
            :key="card.id"
            :rank="card.rank"
            :isFaceUp="card.isFaceUp"
            :class="{'selectable': isPlayerHand}"
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
            default: true
        },
        overlapType: { // 2, 3, 4, 6 work well
            type: Number,
            default: 3
        },
        rotation: { // 0, 1, 2 work well
            type: Number,
            default: 1
        }
    },
    data() {
        return {
            overlapOffset: 20
        }
    },
    computed: {
        rotationOffset() {
            return this.rotation * 30 / Math.max(this.cards.length, 1)
        }
    },
    methods: {
        getCardStyle(index) {
            const numberOfCards = this.cards.length - 1
            return `
                left: ${this.overlapType * this.overlapOffset * (index + .5)}px;
                top: ${25 - Math.sin(Math.PI * index / (Math.max(numberOfCards, 1))) * numberOfCards * 3 * this.rotation}px;
                transform: rotate(${(numberOfCards) * this.rotationOffset * -.5 + index * this.rotationOffset}deg);
            `;
        }
    }
};
</script>

<style lang="scss">
@import "./../style/vars.scss";

.card-hand {
    border-radius: 10px;
    height: $hand-height;
    position: relative;

    .playing-card {
        top: 0;

        &.selectable {
            transition: top 100ms ease;

            &:hover {
                top: $card-hover-top !important;
            }
        }
    }
}
</style>
