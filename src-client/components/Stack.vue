<template>
    <div class="card-stack" @click="go">
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
            default: function() { return [] }
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
                transform: rotate(${this.rotate ? this.rotationOffset[index * 2 % this.rotationOffset.length] : 0}deg);
            `;
        }
    }
};
</script>

<style lang="scss">
@import "./../style/vars.scss";

.card-stack {
    margin: $m-normal;
    border-radius: $card-radius;
    width: $card-width;
    height: $stack-height;
    position: relative;
    display: inline-block;
    border: $card-placeholder-border;

    .playing-card {
        top: 0;

        &.is-player-hand-and-last {
            transition: $card-hover-transition;

            &:hover {
                top: $card-hover-top;
            }
        }
    }
}
</style>
