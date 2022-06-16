<template>
  <div class="p-5 w">
    <h1 class="text-2xl mb-4">Customer list</h1>
    <div class="flex justify-between item m-4">
      <button
        class="bg-green-600 text-white hover:bg-orange-700 rounded-lg w-1/2 p-2"
        @click="addCustomer"
      >
        Add Customer
      </button>
      <div>
        <span>Total: </span>
        <input
          min="0"
          type="number"
          class="border border-gray-700 w-20 text-center"
          v-model="total"
        />
      </div>
    </div>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Part</th>
          <th>Cost</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr class="border-t" v-for="customer in customers" :key="customer.id">
          <td class="p-4 pl-8">
            <div>Person <span v-text="customer.id + 1"></span></div>
          </td>
          <td class="p-4 pl-8">
            <div class="inline-flex gap-2 items-center justify-center">
              <input
                :class="customer.constant ? 'disabled:opacity-75' : ''"
                :disabled="customer.constant"
                type="text"
                class="border border-gray-700 w-20 text-center"
                v-model="customer.part"
                @keyup="calculateRemainderCost"
              />
            </div>
          </td>
          <td class="p-4 pl-8 text-center">
            <input
              min="0"
              type="number"
              class="border border-gray-700 w-20 text-center"
              v-model="customer.cost"
              @keyup="setConstantCost(customer.id)"
              @change="setConstantCost(customer.id)"
            />
          </td>
          <td class="p-4 pl-8">
            <router-link
              :to="`/payment`"
              class="border text-green-600 rounded-lg w-1/2 p-3 mr-2"
            >
              pay
            </router-link>
            <a
              class="border text-red-600 rounded-lg w-1/2 p-3"
              @click="onRemove(customer.id)"
              v-show="customers.length > 1"
            >
              x
            </a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'customer-list',
}
</script>

<script setup>
import { reactive, ref, watch } from 'vue'
const constantCost = ref(0)
const remainderCost = ref(0)
const partPrice = ref(0)
const total = ref(0)

let customers = reactive([
  {
    id: 0,
    product: '',
    part: 1,
    cost: 1,
    constant: false,
  },
])

const setConstantCost = (customerId) => {
  let index = customers.findIndex((customer) => customer.id === customerId)
  customers[index].constant = true
  customers[index].part = '-'

  constantCost.value = customers
    .filter((customer) => customer.constant)
    .map((customer) => customer.cost)
    .reduce((a, b) => a + b, 0)

  calculateRemainderCost()
}

const calculateRemainderCost = () => {
  remainderCost.value = total.value - constantCost.value
  calculatePartPrice()

  customers
    .filter((customer) => !customer.constant)
    .map((customer) => {
      return (customer.cost = partPrice.value * customer.part)
    })
}

const calculatePartPrice = () => {
  partPrice.value =
    remainderCost.value /
    customers
      .map((customer) => {
        return !customer.constant ? customer.part : false
      })
      .reduce((a, b) => a + b, 0)
}

const onRemove = (customerId) => {
  customers.splice(
    customers.findIndex((customer) => customer.id === customerId),
    1
  )

  calculateRemainderCost()
}

const addCustomer = () => {
  customers.unshift({
    id: customers.length,
    product: '',
    part: 1,
    cost: 1,
    constant: false,
  })

  calculateRemainderCost()
}

watch(
  () => total.value,
  (el) => {
    calculateRemainderCost()
  }
)

watch(
  () => customers,
  (el) => {
    calculateRemainderCost()
  }
)
</script>
