<template>
    <div id="tabellone">
        <div :id="'num' + num" class="numero-cella" v-for="num in 90" :key="num">{{ num }}</div>
    </div>
</template>

<script>
export default {
    name: 'Tabellone',
    props:['numeroEstratto','restartTab'],
    data() {
        return {
            numEstratto: this.numeroEstratto,
        }
    },
    watch: {
        numeroEstratto: function(newVal) { //Quando arriva un nuovo numero estratto
            var numPescato = document.getElementById('num' + newVal); //Cerco elemento con id = al numero pescato
            numPescato.classList.add("pescato"); //Aggiungo classe css "Pescato"
        },
        restartTab: function(newVal) { //Quando viene dato l'impulso di restartare
            if(newVal === true) {
                var element = document.getElementsByClassName("numero-cella");

                for(var i = 0; i < element.length; i++) {
                    if(element[i].classList.contains("pescato")) {
                        element[i].classList.remove("pescato");
                    }
                }
            }
        }
    }
}
</script>

<style scoped>
    .numero-cella {
        border: 1px solid black;
        padding: 25px 30px;
        display: inline-block;
        width: 100px;
    }

    .pescato {
        transition: 0.5s;
        background-color: rgba(223, 56, 56, 0.747);
    }
</style>