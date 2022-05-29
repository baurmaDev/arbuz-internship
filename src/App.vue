<template>
  <div>
    <h1>Курчумские Арбузы!</h1>
    <h3>Выберите арбуз с грядки от 1 до 3шт</h3>
    <OrderForm />
  </div>
  
</template>

<script>
import OrderForm from './components/OrderForm.vue'

export default {
  name: 'App',
  components: {
    OrderForm
}
}
</script>

<style>
body{
  background-color: #202020;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffff;
  margin-top: 60px;
  
}
</style>
