<template>
    <div class="card-hand" @click="go">
        <playing-card
            v-for="(card, i) in cards"
            :key="card.id"
            :rank="card.rank"
            :isFaceUp="card.isFaceUp"
            :class="{'is-player-hand-and-last': isPlayerHand && i == cards.length - 1}"
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
        },
        rotate: {
            type: Boolean,
            default: true
        }
    },
    data() {
        return {
            overlapOffset: 110,
            rotationOffset: [-10, -5, 0, 5, 10]
        }
    },
    methods: {
        go() {
            const self = this;
            setInterval(function() {
                self.cards.push({
                    id: self.cards[self.cards.length-1].id + 1,
                    rank: Math.floor(Math.random() * 12),
                    isFaceUp: true
                });
                console.log(self.cards[self.cards.length-1].rank)
            }, 1000);
        },
        getCardStyle(index) {
            return `
                left: ${-1 * this.overlapOffset * index}px;
                // top: ${-Math.sin(Math.PI / (this.cards.length - 1) * index) * this.rotation * this.rotationOffset}px;
                transform: rotate(${this.rotate ? this.rotationOffset[index * 2 % this.rotationOffset.length] : 0}deg);
            `;
        }
    }
};
</script>

<style lang="scss">
.card-stack {
    margin: 16px;
    padding: 6px;
    border-radius: 10px;
    height: 154px;
    overflow: scroll;

    .playing-card {
        position: relative;

        &.is-player-hand-and-last {
            top: 0;
            transition: top 100ms ease;

            &:hover {
                top: -20px;
            }
        }
    }
}
</style>
