<template>
<div>

<ScoreBoard />

    <template v-if="questao">

        <h1 v-html="questao"></h1>

        <template v-for="(resposta, index) in this.respostas" :key="index">
            <input
            :disabled="this.respostaEnviada"
            type="radio" 
            name="options" 
            :value="resposta"
            v-model="respostaEscolhida">
            <label v-html="resposta"></label><br>
        </template>

        <button class="send" type="button"
        v-if="!this.respostaEnviada" @click="enviarResposta()">Enviar</button>

        <section v-if="this.respostaEnviada" class="resultado">
        <h4 v-if="this.respostaEscolhida == this.respostaCorreta"
        v-html="'&#9989; Parabéns você acertou, a resposta correta é  '+respostaCorreta+'!'">
        </h4>
        <h4 v-else
        v-html="'&#10060; Desculpe você errou, a resposta correta é {'+respostaCorreta+'!'">
        </h4>
        <button class="send" type="button" @click="obtemNovaPergunta()">Próximo pergunta</button>
        </section>
    </template>

</div>
</template>

<script>
import ScoreBoard from '@/components/ScoreBoard.vue'

export default {

    name: 'App',
    components: {
      ScoreBoard
    },

    created() {
        this.obtemNovaPergunta()
    },

    //funcao para retornar os dados
    data() {
        //nesse passo analise o que vai precisar e monte seu objeto para receber os dados
        //aqui nao deve ter muito calculos e bla bla bla
        return {
            questao: undefined,
            respostasIncorretas: undefined,
            respostaCorreta: undefined,
            respostaEscolhida: undefined,
            respostaEnviada: false,
        }
    },

    computed: {
        respostas() {
            var respostas = JSON.parse(JSON.stringify(this.respostasIncorretas));
            //random retorna o numero entre 0 e 1 * tamanho do nosso array
            var posicao = Math.round(Math.random() * respostas.length)
            respostas.splice(posicao, 0, this.respostaCorreta);
            return respostas
        }
    },

    methods: {
      obtemNovaPergunta() {
        this.respostaEnviada = false
        this.respostaEscolhida = undefined
        this.questao = undefined
        
        this.axios
            .get('https://opentdb.com/api.php?amount=1&category=18&difficulty=easy')
            .then((response) => {
                this.questao = response.data.results[0].question
                this.respostasIncorretas = response.data.results[0].incorrect_answers
                this.respostaCorreta = response.data.results[0].correct_answer

                console.log(response.data.results[0])
            })

      },
      enviarResposta() {
        if (!this.respostaEscolhida) {
          alert('Escolha uma resposta antes de prosseguir.')
        } else {
          this.respostaEnviada = true
          if(this.respostaEscolhida == this.respostaCorreta) {
            console.log('Parabéns, você acertou!')
          } else {
            console.log('Não foi dessa vez, resposta incorreta!')
          }
        }
      }
    }
}

//URL que será consumida
//https://opentdb.com/api.php?amount=1&category=18&difficulty=easy
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    margin: 60px auto;
    max-width: 960px;

    input[type=radio] {
        margin: 12px 4px;
    }

    button.send {
        margin-top: 12px;
        height: 40px;
        min-width: 120px;
        padding: 0 16px;
        color: #fff;
        background-color: #1667c0;
        border: 1px solid #1667c0;
        cursor: pointer;
    }
}
</style>
