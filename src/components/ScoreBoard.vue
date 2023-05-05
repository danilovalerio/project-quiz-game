<template>
<section class="score">
Jogador <span>{{ this.acertosScore }}</span> x <span>{{ this.errosScore }}</span> Computador
</section>
</template>

<script>
export default {
    //props pode ser declarada com array ou objeto 
    props: ['acertosScore','errosScore']
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
