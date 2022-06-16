<template>
  <div class="about">
    <h1 class="text-2xl my-4">Order</h1>
    <OrderPayment />
  </div>
</template>

<script>
import OrderPayment from '@/components/customers-order'

export default {
  name: 'OrderView',
  components: {
    OrderPayment,
  },
}
</script>
