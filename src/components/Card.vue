<template>
  <article v-if="cardFull.id" class="card" :cardFull="cardFull" :class="cardFull.vendor">
    <header class="header">
      <img src="@/assets/chip-light.svg" alt="chip" />
      <img v-if="cardFull.vendor" :src="require('@/assets/vendor-' + cardFull.vendor + '.svg')" />
    </header>
    <section v-if="Object.keys(cardFull).length !== 0" class="number">
      <h1>
        {{cardFull.cardnumber}}
        <br />
      </h1>
    </section>
    <section class="info">
      <aside class="holder">
        <span>Cardholder:</span>
        <p>{{cardFull.cardholder}}</p>
      </aside>
      <aside class="valid">
        <span>Valid thru:</span>
        <p>{{cardFull.expmonth}}/{{cardFull.expyear}}</p>
      </aside>
    </section>
    <button class="remove" v-if="activeCard" @click="showPopup">Remove Card</button>
    <MyPopup :show="show" @result="alertResult" />
    <!--<a class="remove" href="#" v-if="activeCard" @click="removeCard(cardFull.id)">Remove card</a> -->
  </article>
</template>  
<script>
import MyPopup from '../components/MyPopup.vue'
export default {
  name: "Card",
  props: {
    cardFull: Object,
    activeCard: Boolean,
  }, components: {
    MyPopup
  },
  data () {
    return {
      deleteResponse: false,
      show: false
  }
}, methods: {
  alertResult(payload) {
    this.show = false
    console.log("hej")
    if(payload == true) {
      console.log("hej")
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
h1 {
  font-size: 2vw;
}

.remove {
  text-decoration: none;
  padding: 0.2rem;
  border-radius: 20px;
  font-size: 1em;
  background: linear-gradient(
      0.689turn,
      hsla(0, 100%, 50%, 0.705),
      hsla(19, 100%, 50%, 0.561) 99.07%
    ),
    #ffffff;
}
article {
  margin: 0 auto;
  background: linear-gradient(
      248.3deg,
      hsla(0, 0%, 100%, 0.342),
      hsla(0, 0%, 100%, 0)
    ),
    #222;
  color: #eee;
}
.card {
  width: 24rem;
  height: 14rem;
  border-radius: 0.6rem;
  padding: 1rem;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-box-shadow: 0 0 0.5rem rgba(0, 0, 0, 0.4);
  box-shadow: 0 0 0.5rem rgba(0, 0, 0, 0.4);
  display: grid;
  gap: 0.5rem 0;
  grid-template-columns: 1fr 1fr;
  grid-auto-rows: 2.8rem;
  text-shadow: -1px -1px 2px hsla(0, 0%, 100%, 0.4);
}

.card section aside span {
  display: block;
  text-transform: uppercase;
  font-size: 0.7rem;
  margin: 0 0 0.25rem;
}

.card header {
  -ms-flex-item-align: end;
  align-self: flex-end;
  opacity: 1;
}

.card section aside p {
  display: block;
  text-transform: uppercase;
  margin: 0;
  padding: 0;
}

.card section aside.valid span {
  text-align: right;
}

.card section aside.valid p {
  text-align: right;
}

aside {
  display: block;
}

.holder {
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
}

header {
  display: block;
}

.header {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  grid-column: auto/span 2;
  grid-row: auto/span 2;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: start;
  -ms-flex-align: start;
  align-items: flex-start;
}

.bitcoin {
  background: linear-gradient(
      0.689turn,
      hsla(0, 0%, 100%, 0.15),
      hsla(0, 0%, 100%, 0) 99.07%
    ),
    #ffae34;
  color: #222;
}

.evil {
  background: linear-gradient(248.3deg, rgba(0, 0, 0, 0.16), transparent),
    #f33355;
  color: #fff;
}

.ninja {
  background: linear-gradient(
      248.3deg,
      hsla(0, 0%, 100%, 0.15),
      hsla(0, 0%, 100%, 0)
    ),
    #222;
  color: #fff;
}

.blockchain {
  background: linear-gradient(248.52deg, rgba(0, 0, 0, 0.15) 1.49%, transparent),
    #8b58f9;
  color: #fff;
}

/*img {
  margin-left: 80%;
} */
</style>