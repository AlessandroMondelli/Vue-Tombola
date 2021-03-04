<template>
    <section id="intro">
        <div id="intro-container">
            <h1>Tombola!</h1>
            <button @click="leaveIntro()">Inizia Partita</button>
        </div>
    </section>
</template>

<script>
export default {
    name: 'Intro',
    data() {
        return {
            introStatus: true,
        }
    },
    methods: {
        leaveIntro() {
            this.introStatus = !this.introStatus; //Setto intro a false
            this.$emit('intro-tabella', this.introStatus); //Dico al padre che la intro è false
        }
    }
}
</script>

<style scoped>
#intro {
    width: 95vw;
    height: 85vh;
    display: flex;
}

#intro-container {
    margin: auto;
    text-align: center;
}

h1 {
    font-size: 60px;
    font-weight: 700;
    margin-bottom: 25px;
}

button {
    background-color: rgb(235, 72, 72);
    padding: 10px;
    font-size: 22px;
    transition: 0.2s;
}

button:hover {
    transform: scale(0.98);
    color: black;
    background-color: rgba(231, 35, 35, 0.692);
}
</style>