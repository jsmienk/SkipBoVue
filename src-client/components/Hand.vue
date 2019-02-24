<template>
    <div class="card-hand">
        <playing-card
            v-for="(card, i) in cards"
            :key="card.id"
            :rank="card.rank"
            :isFaceUp="card.isFaceUp"
            :class="{'is-player-hand': isPlayerHand}"
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
        overlapType: { // 0, 1, 2, 3, 4 work well
            type: Number,
            default: 3
        },
        rotation: { // 0, 1, 2 work well
            type: Number,
            default: 2
        }
    },
    data() {
        return {
            overlapOffset: 20,
            rotationOffset: 5
        }
    },
    methods: {
        getCardStyle(index) {
            return `
                left: ${-1 * this.overlapType * this.overlapOffset * index}px;
                top: ${-Math.sin(Math.PI / (this.cards.length - 1) * index) * this.rotation * this.rotationOffset}px;
                transform: rotate(${(this.cards.length - 1) * this.rotation * this.rotationOffset / -2 + index * this.rotation * this.rotationOffset}deg);
            `;
        }
    }
};
</script>

<style lang="scss">
.card-hand {
    padding: 6px;
    border-radius: 10px;
    height: 154px;

    .playing-card {
        position: relative;
    }

    .is-player-hand.playing-card {
        top: 0;
        transition: top 100ms ease;
    }

    .is-player-hand:hover {
        top: -20px !important;
    }
}
</style>
