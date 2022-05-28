<template>
  <div>
    <h1>Hello Arbuz!</h1>
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
