<template>
    <div class="playing-card" :style="style">
        <div>
            <div class="top-rank">{{ rankString }}</div>
            <div>{{ rankMainString }}</div>
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
            faceDownColor: "#555",
            jokerRankName: ['skip', '⁤']
        };
    },
    computed: {
        rankClass() {
            for (const c of this.rankClasses) {
                if (c.range.includes(this.rank)) return c;
            }
        },
        rankMainString() {
            return this.isFaceUp ? this.rank === 0 ? this.jokerRankName[1] : this.rank : '⁤';
        },
        rankString() {
            return this.isFaceUp ? this.rank === 0 ? this.jokerRankName[0] : this.rank : '⁤';
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
    -webkit-user-select: none;  
    -moz-user-select: none;    
    -ms-user-select: none;      
    user-select: none;

    font-weight: bold;
    font-size: 3.5em;
    text-align: center;
    text-transform: uppercase;
    color: #fff;

    // padding: 0 16px 0;
    width: 110px;
    height: 170px;
    padding: 4px 8px;
    border-radius: 10px;
    border: 5px solid #fff;

    .top-rank,
    .bottom-rank {
        font-size: 0.5em;
        text-align: left;
        text-transform: capitalize;
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
