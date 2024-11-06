<script setup>
import { defineProps } from 'vue'

defineProps({
  orderList: Object,
})
const itemSubtotal = item => {
  return item.quantity * item.price
}
</script>

<template>
  <div
    v-if="!orderList.id"
    class="alert alert-secondary text-center"
    role="alert"
  >
    尚未建立訂單
  </div>
  <div v-else class="card">
    <div class="card-body">
      <div class="card-title">
        <h5>訂單</h5>
        <table class="table">
          <thead>
            <tr>
              <th scope="col">品項</th>
              <th scope="col">數量</th>
              <th scope="col">小計</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="order in orderList.cartList" :key="order.id">
              <td>{{ order.name }}</td>
              <td>{{ order.quantity }}</td>
              <td>{{ itemSubtotal(order) }}</td>
            </tr>
          </tbody>
        </table>
        <div class="text-end">
          備註: <span>{{ orderList.description || '無' }}</span>
        </div>
        <div class="text-end">
          <h5>
            總計: <span>${{ orderList.total }}</span>
          </h5>
        </div>
      </div>
    </div>
  </div>
</template>
