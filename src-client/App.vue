<template>
    <div id="app">
        <Header>SkipBo</Header>
        <playing-card :rank="0"/>
        <playing-card :rank="4"/>
        <playing-card :rank="8"/>
        <playing-card :rank="8" :isFaceUp="false"/>
        <playing-card :rank="10"/>
        <Footer/>
    </div>
</template>

<script>
import Header from "./components/Header.vue"
import Footer from "./components/Footer.vue"
import PlayingCard from "./components/PlayingCard.vue"

export default {
    name: "app",
    components: {
        Header, Footer, PlayingCard
    },
    data() {
        return {}
    }
};
</script>

<style lang="scss">
* {
    box-sizing: border-box;
}

html, body {
    margin: 16px;
    background-color: #222;
    color: #efefef;
}
</style>
