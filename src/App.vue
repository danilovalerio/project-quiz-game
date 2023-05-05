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
  components: {
    
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
