<template>
  <div class="home">
    <Top :topMessage="topMessage" :activeCard="activeCard" />
    <Card :cardFull="cardFull" @removeCard="removeCard" :activeCard="activeCard" />
    <CardStack :cards="cards" @showCard="showCard" />
  </div>
</template>

<script>
import Top from '../components/Top.vue'
import Card from '../components/Card.vue'
import CardStack from '../components/CardStack.vue'

export default {
  name: 'Home',
  data () {
    return {
      topMessage: "E-Wallet",
      activeCard: true,
      cardFull: {
          
        }
    }
  },
  components: {
    Top,
    Card, 
    CardStack
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
    }
  }   
}
</script>
