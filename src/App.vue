<template>
  <section>
    <Header/>
    <div id="container">
      <div v-if="!gameOver" id="in-game">
        <generate-number @estrai-numero="estraiNumeroTabellone" @game-over="getGameOver" @restart-game="restartGame"></generate-number>
        <tabella></tabella>
        <tabellone :numeroEstratto="numeroEstrattoTabellone" :restartTab="restart"></tabellone>
      </div>
      <div v-else id="game-over">
        <h2>Game Over</h2>
      </div>
    </div>
  </section>
</template>

<script>
import Header from './components/Header.vue';
import GenerateNumber from './components/GenerateNumber.vue';
import Tabellone from './components/Tabellone.vue';
import Tabella from './components/Tabella.vue'

export default {
  name: 'App',
  components: {
    Header,
    GenerateNumber,
    Tabellone,
    Tabella,
  },
  data() {
    return {
      numeroEstrattoTabellone: '',
      gameOver: false,
      restart: false,
    }
  },
  methods: {
    estraiNumeroTabellone(num) { //Prendo numero al click su "Estrai numero"(Dato preso dal component "GenerateNumber con emits")
      this.numeroEstrattoTabellone = num; //Assegno dato a variabile locale
    },
    getGameOver(val) { //Prendo valore inviato con $emits da GenerateNumber
      this.gameOver = val; //Setto valore a variabile locale
    },
    restartGame(val) {//Prendo valore inviato con $emits da GenerateNumber
      this.restart = val; //Setto valore a variabile locale
    }
  },
}
</script>

<style>
* {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

html {
  background-color: #E9E9E9;
}

#container {
  width: 90%;
  margin: auto;
  padding-top: 50px;
  height: 70vh;
}
</style>
