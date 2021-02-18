<template>
    <div id="create-tabellina">
    <button id="gen-tabella" @click="createTab(),genTab = !genTab" v-if="!genTab">Genera Tabella</button>
    <div v-else id="tabella" ref="draggableContainer" class="draggable-container">
        <div id="tabellina"  class="draggable-header" @mousedown="dragMouseDown">
            <button id="el-tabella" @click="tabellina = [],genTab = !genTab">Elimina Tabella</button>
            <!--<div :id="'riga' + num" class="riga-tabellina" v-for="num in 3" :key="num"> 
                <div :id="'pos' + num" class="numero-tabellina" v-for="num in 9" :key="num"></div>
            </div> -->
            <h2>La tua Tabella</h2>
            <div class="cella-tabellina" :id="numTabella" v-for="numTabella in tabellina" :key="numTabella">{{ numTabella }}</div>
        </div>
    </div>
    </div>
</template>

<script>
export default {
    name: 'Tabella',
    props:['numeroEstrattoTabellina'],
    data() {
        return {
            numEstratto: this.numeroEstrattoTabellina,
            resTab: false,
            genTab: false,
            tabellina: [],
            positions: {
                clientX: undefined,
                clientY: undefined,
                movementX: 0,
                movementY: 0
            }
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
        dragMouseDown: function (event) {
            event.preventDefault()
            // get the mouse cursor position at startup:
            this.positions.clientX = event.clientX
            this.positions.clientY = event.clientY
            document.onmousemove = this.elementDrag
            document.onmouseup = this.closeDragElement
        },
        elementDrag: function (event) {
            event.preventDefault()
            this.positions.movementX = this.positions.clientX - event.clientX
            this.positions.movementY = this.positions.clientY - event.clientY
            this.positions.clientX = event.clientX
            this.positions.clientY = event.clientY
            // set the element's new position:
            this.$refs.draggableContainer.style.top = (this.$refs.draggableContainer.offsetTop - this.positions.movementY) + 'px'
            this.$refs.draggableContainer.style.left = (this.$refs.draggableContainer.offsetLeft - this.positions.movementX) + 'px'
            },
        closeDragElement () {
            document.onmouseup = null
            document.onmousemove = null
        }
    },
    watch: {
        numeroEstrattoTabellina: function(newVal) { //Guardo numero estratto tabellone
            console.log('1');
            if(this.tabellina.includes(newVal)) { //Se è presente nella tabellina
                var numPescatoTabellina = document.getElementById(newVal); //Cerco elemento con id = al numero pescato
                numPescatoTabellina.classList.add("pescato"); //Aggiungo classe css "Pescato"
            }
        }
    }
}
</script>

<style scoped>
    button {
        border: 1px solid rgb(61, 110, 167);
        background-color:rgb(61, 110, 167);
        position: absolute;
    }

    #gen-tabella {
        border: 1px solid rgb(61, 110, 167);
        background-color:rgb(61, 110, 167);
    }

    #el-tabella {
        border: 1px solid rgb(202, 84, 63);
        background-color:rgb(179, 82, 65);
        padding: 10px;
        position: relative;
        left: 75%;
    }

    #tabella {
        cursor: grab;
        background-color: rgba(253, 253, 253, 0.733);
        
    }

    .riga-tabellina {
        display: block;
        border: 1px solid black;
        padding: 20px;
        background-color: rgba(233, 231, 231, 0.418);
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

    .pescato {
        transition: 0.2s;
        background-color: rgba(177, 73, 55, 0.527);
    }

    .draggable-container {
        position: absolute;
        z-index: 9;
        width: 25%;
    }

    .draggable-header {
        z-index: 10;
    }
</style>