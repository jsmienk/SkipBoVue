<template>
  <div id="app">
    <Header>SkipBo</Header>
    <Hand :cards="cards"/>
    <Stack :cards="cards"/>
    <Stack :cards="cards" :isPlayerHand="true" :rotate="false"/>
    <Stock :cards="cards" :isPlayerHand="false"/>
    <Footer/>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Hand from "./components/Hand.vue";
import Stack from "./components/Stack.vue";
import Stock from "./components/Stock.vue";

export default {
  name: "app",
  components: {
    Header,
    Footer,
    Hand,
    Stack,
    Stock
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
        },
        {
          id: 5,
          rank: 9,
          isFaceUp: true
        },
        {
          id: 6,
          rank: 6,
          isFaceUp: true
        },
        {
          id: 7,
          rank: 2,
          isFaceUp: true
        }
      ]
    };
  }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html,
body {
  margin: 16px;
  background-color: #222;
  color: #efefef;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
