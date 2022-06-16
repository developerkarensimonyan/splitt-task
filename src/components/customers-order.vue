<template>
  <div class="flex justify-around">
    <CustomerList />
  </div>
</template>

<script>
import CustomerList from '@/components/customer-list'

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'customers-order',
  components: {
    CustomerList,
  },
}
</script>
