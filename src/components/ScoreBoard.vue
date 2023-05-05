<template>
<section class="score">
Jogador <span>{{ this.acertosContador }}</span> x <span>{{ this.errosContador }}</span> Computador
</section>
</template>

<script>
export default {
    //props pode ser declarada com array ou objeto 
    props: ['acertosContador','errosContador']
}
</script>

<style lang="scss">
section.score {
    border-bottom: 1px solid black;
    padding: 24px;
    font-size: 18px;

    span {
        padding: 8px;
        font-weight: bold;
        border: 1px solid black;
    }
}

</style>
