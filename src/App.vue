<template>
  <div>
  <h1>Questão 1</h1>
  </div>

  <input type="radio" name="options" value="True">
  <label>True</label><br>

  <input type="radio" name="options" value="False">
  <label>False</label><br>

  <button class="send" type="button">Enviar</button>
  
</template>

<script>

export default {
  name: 'App',

  //funcao para retornar os dados
  data(){
    //nesse passo analise o que vai precisar e monte seu objeto para receber os dados
    return {
      questao: undefined,
      respostasIncorretas: undefined,
      respostaCorreta: undefined
    }
  },

  created() {
    this.axios
    .get('https://opentdb.com/api.php?amount=1&category=18&difficulty=easy')
    .then((response) => {
      this.questao = response.data.results[0].question
      this.respostasIncorretas = response.data.results[0].incorrect_answers
      this.respostaCorreta = response.data.results[0].correct_answer
       
      console.log(response.data.results[0])
      })
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
