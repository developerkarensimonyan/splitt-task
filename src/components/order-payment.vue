<template>
  <h1 class="text-2xl my-4">Payment</h1>
  <div class="max-w-xl mx-auto bg-white py-8 px-8">
    <div class="flex justify-between border-b">
      <div class="items-center p-2 rounded-md">Total</div>
      <div
        class="items-center p-2 rounded-md text-2xl"
        v-text="props.amount + ' $'"
      />
    </div>
    <div>
      <div class="items-center p-2 rounded-md my-4">Payment Systems</div>
      <div class="flex justify-between">
        <router-link
          class="bg-orange-600 text-white hover:bg-orange-700 rounded-lg w-1/2 p-3 mr-3"
          :to="'/payment-details'"
          >PayPal
        </router-link>
        <router-link
          class="bg-orange-600 text-white hover:bg-orange-700 rounded-lg w-1/2 p-3"
          href="/payment-details"
          :to="'/payment-details'"
          >Credit Card
        </router-link>
      </div>
    </div>
  </div>
  <router-link :to="`/`" class="border text-black rounded-lg w-1/2 p-3">
    back
  </router-link>
</template>

<script>
export default {
  name: 'order-payment',
}
</script>

<script setup>
// eslint-disable-next-line no-undef
const props = defineProps({
  amount: {
    type: Number,
  },
  owner: {
    type: String,
  },
})
</script>
