<template>
    <div id="generate-num">
        <button @click="estraiNumero">Estrai un numero</button>
        <div id="num-estr">
            <p v-if="numeroEstratto != ''" class="last-estr-par">Ultimo numero estratto</p>
            <p class="last-estr-num"> {{ numeroEstratto }} </p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'GenerateNumber',
  data() {
        return {
        numeroEstratto: '',
        numeriEstratti: [],
        gameOver: false,
        }
  },
  methods: {
        estraiNumero() {
            var flag = false; //Flag che verifica estrazione di un numero non già uscito

            do { //Ciclo do while finchè..
                this.numeroEstratto = Math.floor(Math.random() * (90 - 1 + 1) ) + 1; //Estraggo un numero casuale da 1 a 90

                if (!this.numeriEstratti.includes(this.numeroEstratto)) { //Se il numero non è incluso nell'array dei numeri estratti
                    this.$emit('estrai-numero', this.numeroEstratto); //Invio numero a component
                    this.numeriEstratti.push(this.numeroEstratto); //Inserisco numero in array

                    flag = true; //Setto flag a true, terminando il ciclo
                }
            } while(flag === false); //Il numero è già stato estratto
        }
  },
   watch: {
         numeriEstratti: { //watch su array dei numeri estratti
            handler: function () {
                if(this.numeriEstratti.length == 90) { //se l'array raggiunge i 90 numeri
                    this.gameOver = true; //Game over
                    this.$emit('game-over', this.gameOver); //Invio numero a component
                }
            },
            deep: true
        }
   }
}
</script>

<style scoped>
#generate-num {
    margin-bottom: 30px;
}

#num-estr {
    display: inline-block;
    margin-left: 45px;
}

button {
    display: inline-block;
    vertical-align: text-bottom;
    background: none;
	color: white;
	border: 1px solid #CC5151;
    border-radius: 5px;
    background-color:rgb(204,81,81);
	padding: 20px;
	font: inherit;
	cursor: pointer;
	outline: inherit;
    transition: 0.2s;
}

button:hover {
    background-color:rgba(204,81,81,0.4);
    transform: scale(0.98);
}

.last-estr-par {
    font-size: 22px;
    font-weight: bold;
}

.last-estr-num {
    font-size: 28px;
    font-weight: bold;
}
</style>