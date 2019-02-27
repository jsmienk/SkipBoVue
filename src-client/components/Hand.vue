<template>
    <div class="card-hand" :class="{'is-enemy': !isUser}">
        <playing-card
            v-for="(card, i) in cards"
            :key="card.id"
            :rank="card.rank"
            :isFaceUp="isUser"
            :isSmall="!isUser"
            :class="{selectable: isUser}"
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
        isUser: {
            type: Boolean,
            default: true
        },
        rotation: {
            type: Boolean,
            default: true
        }
    },
    data() {
        return {
            overlapOffset: 20
        }
    },
    computed: {
        rotationOffset() {
            return this.rotation * 30 / Math.max(this.cards.length, 1);
        },
        overlapType() {
            return this.isUser ? 3 : 1;
        }
    },
    methods: {
        getCardStyle(index) {
            const lastIndex = this.cards.length - 1;
            // Card offset from the left side
            const upsideDownCompensation = this.isUser ? 0 : (lastIndex + 4) * this.overlapOffset;
            const leftOffset = this.overlapType * this.overlapOffset * (index + .5);
            // Card offset from the top follows a wave pattern
            const top = 25 - Math.sin(Math.PI * index / (Math.max(lastIndex, 1))) * lastIndex * 3 * this.rotation;
            // Rotation from left to right
            const rot = (lastIndex) * this.rotationOffset * -.5 + index * this.rotationOffset;

            return `
                left: ${leftOffset - upsideDownCompensation}px;
                top: ${top}px;
                transform: rotate(${rot}deg);
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
    display: inline-block;

    &.is-enemy {
        height: $hand-small-height;
        transform: rotate(180deg);
    }

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
