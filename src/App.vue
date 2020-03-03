<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>|
      <router-link to="/AddCard">Add Credit Card</router-link>
    </div>
    <router-view :cards="cards" @addCard="addCard" @removeCard="removeCard" />
  </div>
</template>
<script>
export default {
  name: "App",
  data () {
       return {
         cards:
    [
      /*{id: 1, cardnumber: "0909 3994 4224", cardholder: "Krongie Brongersson", expyear: "10", expmonth: "02", ccv: "885", vendor: "bitcoin"},
      {id: 2, cardnumber: "2229 4444 3333", cardholder: "Jack Jackman", expyear: "22", expmonth: "12", ccv: "442", vendor: "blockchain"},
      {id: 3, cardnumber: "4432 4674 8594", cardholder: "Hans Hansson", expyear: "05", expmonth: "06", ccv: "223", vendor: "evil"},
      {id: 4, cardnumber: "9020 2299 3340", cardholder: "Kluck Chickman", expyear: "08", expmonth: "11", ccv: "223", vendor: "ninja"} */
    ]           
}}, 
  methods: {
  // Hantera all CRUD här. Där man lägger till kort
   addCard(payload) {
    this.cards.push(payload);
  }, removeCard(id) {
    console.log(id);
    this.cards.splice(id - 1, 1)
    for(let i = 0; i < this.cards.length; i++) {
      this.cards[i].id = i + 1
      console.log(this.cards[i].id)
    }
    location.reload();
  }
}, watch: {
  cards: {
    handler() { console.log('Cards changed!');
    localStorage.setItem('cards', JSON.stringify(this.cards));
    },
    deep: true,
  },
}, mounted() {
  console.log('App mounted!');
  if (localStorage.getItem('cards')) this.cards = JSON.parse(localStorage.getItem('cards'));
},
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
