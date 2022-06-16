<template>
  <div class="flex justify-center items-center min-h-screen">
    <div class="h-auto w-80 bg-white p-3 rounded-lg">
      <order-payment :amount="10" :owner="'poxos'" />
    </div>
  </div>
</template>

<script>
import OrderPayment from '@/components/order-payment'

export default {
  name: 'PaymentView',
  components: {
    OrderPayment,
  },
}
</script>
