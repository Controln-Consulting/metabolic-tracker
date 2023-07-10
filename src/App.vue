<script setup>
import OrderTracker from './components/OrderTracker.vue'

</script>

<template>
  <header>
    <h1>Order Tracker</h1>

    <div class="wrapper">
      <OrderTracker msg="You did it!" />
    </div>
  </header>

</template>

<style scoped>
h1  {
  width: fit-content;
  margin: 0 auto;
  text-align: center;
}
</style>
