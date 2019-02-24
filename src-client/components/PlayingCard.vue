<template>
    <div class="playing-card" :style="style">
        <div>
            <div class="top-rank">{{ rankString }}</div>
            <div>{{ rankString }}</div>
            <div class="bottom-rank">{{ rankString }}</div>
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
            faceDownColor: "#555"
        };
    },
    computed: {
        rankClass() {
            for (const c of this.rankClasses) {
                if (c.range.includes(this.rank)) return c;
            }
        },
        rankString() {
            return this.isFaceUp ? this.rank : '⁤';
        },
        style() {
            return `
                background-color: ${this.isFaceUp ? this.rankClass.color : this.faceDownColor};
            `;
        }
    }
};
</script>

<style lang="scss">
.playing-card {
    display: inline-block;

    font-weight: bold;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 3em;
    text-align: center;
    color: #fff;

    // padding: 0 16px 0;
    width: 90px;
    height: 140px;
    padding: 4px 8px;
    border-radius: 10px;
    border: 4px solid #fff;

    .top-rank,
    .bottom-rank {
        font-size: 0.4em;
        text-align: left;
    }

    .top-rank {
        margin-bottom: 12px;
    }

    .bottom-rank {
        transform: rotate(180deg);
        margin-top: 12px;
    }
}
</style>
