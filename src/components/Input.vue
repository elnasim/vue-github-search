<template>
  <form class="input-wrapper" @submit.prevent="getData(inputData)">
    <input class="input" type="text" placeholder="Введите имя пользователя..." v-model="inputData" @input="getData(inputData)">
    <!--<button class="input-btn">Искать</button>-->
  </form>
</template>

<script>
  export default {
    name: "Input",
    props: ['getData'],
    data() {
      return {
        inputData: ''
      }
    },
    methods: {}
  }
</script>

<style scoped lang="scss">
  .input {
    width: 100%;
    padding: 10px;
    font-size: 24px;
  }

  .input-wrapper {
    display: flex;
  }

  .input-btn {
    min-width: 200px;
    margin-left: 5px;
    border: none;
    background-color: #567842;
    color: #ffffff;
    font-size: 27px;
    cursor: pointer;
  }
</style>
