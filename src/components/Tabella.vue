<template>
    <div id="tabella">
        <button id="gen-tabella" @click="createTab(),genTab = !genTab" v-if="!genTab">Genera Tabella</button>
        <div id="tabellina" v-else>
            <button id="el-tabella" @click="tabellina = [],genTab = !genTab">Elimina Tabella</button>
            <!--<div :id="'riga' + num" class="riga-tabellina" v-for="num in 3" :key="num"> 
                <div :id="'pos' + num" class="numero-tabellina" v-for="num in 9" :key="num"></div>
            </div> -->
            <h2>La tua Tabella</h2>
            <div class="cella-tabellina" v-for="numTabella in tabellina" :key="numTabella">{{ numTabella }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Tabella',
    data() {
        return {
            resTab: false,
            genTab: false,
            tabellina: [],
        }
    },
    methods: {
        createTab() {
            for (var i = 0; i < 15; i++) {
                var flag = false; //Flag che verifica estrazione di un numero non già uscito

                
                do { //Ciclo do while finchè..
                    var numeroTabellina = Math.floor(Math.random() * (90 - 1 + 1) ) + 1; //Estraggo un numero casuale da 1 a 90

                    if ((!this.tabellina.includes(numeroTabellina))) { //Se il numero non è incluso nell'array dei numeri estratti
                        this.tabellina.push(numeroTabellina); //Inserisco numero in array
                        flag = true; //Setto flag a true, terminando il ciclo

                        this.tabellina.sort((a, b) => a - b);
                    }
                } while(flag === false); //Il numero è già stato estratto
            }
        },
    }
}
</script>

<style scoped>
    button {
        display: inline-block;
        vertical-align: text-bottom;
        background: none;
        color: white;
        border: 1px solid rgb(61, 110, 167);
        border-radius: 5px;
        background-color:rgb(61, 110, 167);
        padding: 20px;
        font: inherit;
        cursor: pointer;
        outline: inherit;
        transition: 0.2s;
    }

    #gen-tabella {
        border: 1px solid rgb(61, 110, 167);
        background-color:rgb(61, 110, 167);
    }

    #el-tabella {
        border: 1px solid rgb(202, 84, 63);
        background-color:rgb(179, 82, 65);
    }

    #tabella {
        top: 35%;
        width: 30%;
        margin-bottom: 20px;
    }

    .riga-tabellina {
        display: block;
        border: 1px solid black;
        padding: 20px;
    }

    .numero-tabellina {
        display: inline-block;
        border: 1px solid black;
        width: 10.5%;
        padding: 20px 0;
    }

    #tabellina {
        display: block;
        border: 1px solid black;
        padding: 20px;
    }

    .cella-tabellina {
        display: inline-block;
        border: 1px solid black;
        width: 10%;
        padding: 20px;
    }
</style>