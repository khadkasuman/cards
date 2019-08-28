<template lang='pug'>
  div
    div.title Draw Card
    div
      img(:src='img')
    button(@click='drawNow') Draw
</template>

<script>
export default {
  data() {
    return {
      img: "",
      deckId: "68xs0rb9rjgi"
    };
  },
  methods: {
    async drawNow() {
      const res = await this.$http.$get(
        `https://deckofcardsapi.com/api/deck/${this.deckId}/draw/?count=1`
      );
      if (res.cards.length > 0) {
        this.img = res.cards[0].image;
      } else {
        const newDeck = await this.$http.$get(
          "https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1"
        );
        this.deckId = newDeck.deck_id;
        await this.drawNow();
      }
    }
  }
};
</script>

<style scoped>
.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 400;
  font-size: 100px;
  color: #2E495E;
  letter-spacing: 1px;
  font-size: 6em;
}
.green {
  color: #00C48D;
}

.subtitle {
  font-weight: 300;
  font-size: 3em;
  color: #2E495E;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
