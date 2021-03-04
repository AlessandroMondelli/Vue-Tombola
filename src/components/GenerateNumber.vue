<template>
    <section id="generate-num">
        <button v-if="numeriEstratti.length < 90" @click="estraiNumero">Estrai un numero</button>
        <div v-if="numeroEstratto != ''" id="num-estr">
            <p class="last-estr-par">Ultimo numero estratto</p>
            <p class="last-estr-num"> {{ numeroEstratto }} </p>
        </div>
        <div id="restart">
            <button v-if="gameStarted" @click="restartGame">Pulisci Tabellone</button>
        </div>
    </section>
</template>

<script>
export default {
  name: 'GenerateNumber',
  data() {
        return {
            numeroEstratto: '',
            numeriEstratti: [],
            gameStarted: false,
            restart: false,
        }
  },
  methods: {
        estraiNumero() {
            this.gameStarted = true; //Variabile che verifica che segnala la partita come iniziata
            this.$emit('game-started', this.gameStarted); //Invio al padre segnale che la partita è iniziata

            var flag = false; //Flag che verifica estrazione di un numero non già uscito

            if(this.restart) { //Se restart è settato su "true"
                this.restart = false;
                this.$emit('restart-game', this.restart); //Dico al padre che restart è false
            }

            do { //Ciclo do while finchè..
                this.numeroEstratto = Math.floor(Math.random() * (90 - 1 + 1) ) + 1; //Estraggo un numero casuale da 1 a 90

                if (!this.numeriEstratti.includes(this.numeroEstratto)) { //Se il numero non è incluso nell'array dei numeri estratti
                    this.$emit('estrai-numero', this.numeroEstratto); //Invio numero a component
                    this.numeriEstratti.push(this.numeroEstratto); //Inserisco numero in array

                    flag = true; //Setto flag a true, terminando il ciclo
                }
            } while(flag === false); //Il numero è già stato estratto
        },
        restartGame() {
            this.numeriEstratti = [];
            this.numeroEstratto = '';
            this.gameStarted = false; //Variabile che verifica che segnala la partita come iniziata
            this.$emit('game-started', this.gameStarted); //Invio al padre segnale che la partita è iniziata
            this.restart = true;
            this.$emit('restart-game', this.restart); //Invio segnale di restart
        }
  }
}
</script>

<style scoped>
#generate-num {
    margin-bottom: 30px;
}

#num-estr {
    text-align: center;
    display: block;
    width: 24%;
    border: 1px solid rgba(0, 0, 0, 0.363);
    border-radius: 3px;
    padding: 10px;
    box-shadow: 0 2px 8px rgba(104, 104, 104, 0.288);
    margin: 20px 0;
}

#restart {
    display: block;
}

#restart button {
    background-color: rgb(99, 209, 99);
    border: none;
}

button {
	border: 1px solid #CC5151;
    background-color:rgb(204,81,81);
}

button:hover {
    background-color:rgba(204,81,81,0.4);
    transform: scale(0.95);
}

.last-estr-par, .last-estr-num  {
    font-weight: bold;
}

.last-estr-par {
    font-size: 22px;
}

.last-estr-num {
    font-size: 28px;
}
</style>