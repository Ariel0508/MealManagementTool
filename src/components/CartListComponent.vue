<script setup>
import { defineProps, defineEmits } from 'vue'
defineProps({
  cartList: Array,
  total: Number,
  description: String,
})

const emit = defineEmits([
  'removeDrink',
  'updateQty',
  'createOrder',
  ['update:description'],
])
const removeDrink = id => {
  emit('removeDrink', id)
}
const updateQty = drink => {
  emit('updateQty', drink)
}
const itemSubtotal = item => {
  return item.quantity * item.price
}
const createOrder = () => {
  emit('createOrder')
}
</script>

<template>
  <table class="table">
    <thead>
      <tr>
        <th scope="col" width="50">操作</th>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col" width="90">數量</th>
        <th scope="col">單價</th>
        <th scope="col">小計</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="drink in cartList" :key="drink.id">
        <td>
          <button
            type="button"
            class="btn btn-sm"
            @click="removeDrink(drink.id)"
          >
            x
          </button>
        </td>
        <td>{{ drink.name }}</td>
        <td>
          <small>{{ drink.description }}</small>
        </td>
        <td>
          <select
            class="form-select"
            v-model="drink.quantity"
            @change="updateQty(drink)"
          >
            <option v-for="i in 10" :key="i" :value="i">{{ i }}</option>
          </select>
        </td>
        <td>{{ drink.price }}</td>
        <td>{{ itemSubtotal(drink) }}</td>
      </tr>
    </tbody>
  </table>
  <div
    v-if="cartList.length === 0"
    class="alert alert-primary text-center"
    role="alert"
  >
    請選擇商品
  </div>
  <div v-else>
    <div class="text-end mb-3">
      <h5>
        總計: <span>${{ total }}</span>
      </h5>
    </div>
    <textarea
      class="form-control mb-3"
      rows="3"
      placeholder="備註"
      :value="description"
      @input="$emit('update:description', $event.target.value)"
    ></textarea>
    <div class="text-end">
      <button class="btn btn-primary" @click.prevent="createOrder">送出</button>
    </div>
  </div>
</template>
