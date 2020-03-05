<template>
  <div class="home">
    <Top :topMessage="topMessage" :activeCard="activeCard" />
    <Card :cardFull="cardFull" @removeCard="removeCard" :activeCard="activeCard" />
    <button class="remove" v-if="this.cardFull.id" @click="showPopup">Remove Card</button>
    <MyPopup :show="show" @result="alertResult" />
    <CardStack :cards="cards" @showCard="showCard" />
  </div>
</template>

<script>
import Top from '../components/Top.vue'
import Card from '../components/Card.vue'
import CardStack from '../components/CardStack.vue'
import MyPopup from '../components/MyPopup.vue'

export default {
  name: 'Home',
  data () {
    return {
      topMessage: "E-Wallet",
      activeCard: true,
      deleteResponse: false,
      show: false,
      cardFull: {
          
        }
    }
  },
  components: {
    Top,
    Card, 
    CardStack,
    MyPopup
  },
  props: {
    cards: Array
  },
  methods: {
    showCard(payload) {
      this.cardFull = payload;
    },
    removeCard(payload) {
      this.$emit('removeCard', payload)
    },
    alertResult(payload) {
    this.show = false
    if(payload == true) {
      this.$emit('removeCard', this.cardFull.id)
    }
  },
    showPopup() {
    this.show = true;
    }
}
}
</script>
<style scoped>
.remove {
  margin-top: 1%;
  text-decoration: none;
  padding: 0.5rem;
  border-radius: 20px;
  font-size: 1em;
  background: linear-gradient(
      0.689turn,
      hsla(0, 100%, 50%, 0.705),
      hsla(19, 100%, 50%, 0.561) 99.07%
    ),
    #ffffff;
}
</style>
