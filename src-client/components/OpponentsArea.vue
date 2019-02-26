<template>
    <div class="opponents-area">
        <PlayerArea 
            v-for="(enemy, i) in enemies" 
            :key="i"
            :isPlayersArea="false"
        />
    </div>
</template>

<script>
import PlayerArea from "./PlayerArea.vue";

export default {
    components: {
        PlayerArea
    },
    props: {
        enemies: {
            type: Array,
            default: function() { return [{}, {}, {}] }
        }
    },
    data() {
        return {}
    }
}
</script>

<style lang="scss">
.opponents-area {
    display: flex;
    align-items: center;
}
</style>
