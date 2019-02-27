<template>
    <div id="game">
        <OpponentsArea/>
        <TowerArea/>
        <PlayerArea/>
    </div>
</template>

<script>
import OpponentsArea from "./OpponentsArea.vue";
import TowerArea from "./TowerArea.vue";
import PlayerArea from "./PlayerArea.vue";

export default {
    components: {
        OpponentsArea,
        TowerArea,
        PlayerArea
    },
    props: {},
    data() {
        return {}
    }
}
</script>

<style lang="scss">
#game {
    
}
</style>
