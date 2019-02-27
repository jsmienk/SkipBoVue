<template>
  <div id="app">
    <Header>SkipBo</Header>
    <Game/>
    <Footer/>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Game from "./components/Game.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "app",
  components: {
    Header,
    Game,
    Footer
  },
  data() {
    return {
      cards: [
        {
          id: 0,
          rank: 12,
          isFaceUp: true
        },
        {
          id: 1,
          rank: 3,
          isFaceUp: true
        },
        {
          id: 2,
          rank: 8,
          isFaceUp: true
        },
        {
          id: 3,
          rank: 9,
          isFaceUp: true
        },
        {
          id: 4,
          rank: 0,
          isFaceUp: true
        }
      ]
    };
  }
};
</script>

<style lang="scss">
@import "./style/vars.scss";

* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  background-color: $black;
  color: $white;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
