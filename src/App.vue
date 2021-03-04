<template>
  <section>
    <Intro @intro-tabella="leaveIntro" v-if="intro"></Intro>
    <div v-else id="container">
      <Header/>
      <div id="in-game">
        <generate-number id="gen-numb" @estrai-numero="estraiNumeroTabellone" @restart-game="restartGame" @game-started="gameStarted"></generate-number>
        <tabella :numeroEstrattoTabellina="numeroEstrattoTabellone" :gameStart="gameStart"></tabella>
        <tabellone id="tab" :numeroEstratto="numeroEstrattoTabellone" :restartTab="restart"></tabellone>
      </div>
    </div>
  </section>
</template>

<script>
import Intro from './components/Intro.vue';
import Header from './components/Header.vue';
import GenerateNumber from './components/GenerateNumber.vue';
import Tabellone from './components/Tabellone.vue';
import Tabella from './components/Tabella.vue'

export default {
  name: 'App',
  components: {
    Intro,
    Header,
    GenerateNumber,
    Tabellone,
    Tabella,
  },
  data() {
    return {
      numeroEstrattoTabellone: '',
      intro: true,
      gameStart: false,
      restart: false,
    }
  },
  methods: {
    leaveIntro(val) { //Prendo valore Intro
      this.intro = val;
    },
    estraiNumeroTabellone(num) { //Prendo numero al click su "Estrai numero"(Dato preso dal component "GenerateNumber con emits")
      this.numeroEstrattoTabellone = num; //Assegno dato a variabile locale
    },
    gameStarted(val) { //Prendo valore inviato con $emits da GenerateNumber per verificare che la partita sia iniziata
      this.gameStart = val;
    },
    restartGame(val) { //Prendo valore inviato con $emits da GenerateNumber
      this.restart = val; //Setto valore a variabile locale
    }
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,300&display=swap');

* {

  font-family: 'Lato', sans-serif;
}

html {
  background-color: #E9E9E9;
}

#container {
  width: 90%;
  margin: auto;
  padding-top: 50px;
}

button {
  display: inline-block;
  vertical-align: text-bottom;
  background: none;
	color: white;
  border-radius: 5px;
	padding: 15px;
	font: inherit;
	cursor: pointer;
	outline: inherit;
  transition: 0.2s;
}

#in-game {
  display: flex;
  align-items: center;
  position: relative;
}

#gen-numb {
  float: left;
  width: 30%;
  
}

#tab {
  float: left;
  width: 70%;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
