<script setup>
import { ref, computed } from 'vue'
import ProductListComponent from '@/components/ProductListComponent.vue'
import CartListComponent from '@/components/CartListComponent.vue'
import OrderListComponent from '@/components/OrderListComponent.vue'
// import OrderListComponent from '@/components/OrderListComponent.vue';
const data = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
  },
])
const cartList = ref([])
const orderList = ref({})
const description = ref('')
//選取品項加入 cartList
const addCart = drink => {
  // 若沒有品項則新增品項，有品項則新增數量
  const item = cartList.value.find(item => item.name === drink.name)
  if (!item) {
    cartList.value.push({
      ...drink,
      id: new Date().getTime(),
      quantity: 1,
    })
  } else {
    item.quantity++
  }
  console.log(cartList)
}
// 將數量變成動態的數字
const updateQty = drink => {
  cartList.value = cartList.value.map(item => {
    if (item.id === drink.id) {
      item.quantity = +drink.quantity
    }
    return item
  })
  console.log(cartList)
}
// 計算總金額
const total = computed(() => {
  return cartList.value.reduce((pre, item) => {
    return pre + item.quantity * item.price
  }, 0)
})
// 刪除品項
const removeDrink = id => {
  cartList.value = cartList.value.filter(item => item.id !== id)
}
//送出加入 orderList
const createOrder = () => {
  orderList.value = {
    id: new Date().getTime(),
    description: description.value,
    cartList: cartList.value,
    total: total.value,
  }
  cartList.value = []
  description.value = ''
}
</script>
<template>
  <div id="root">
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-4">
          <div class="list-group">
            <ProductListComponent :data="data" @add-cart="addCart" />
          </div>
        </div>
        <div class="col-md-8">
          <CartListComponent
            :cartList="cartList"
            :description="description"
            :total="total"
            @remove-drink="removeDrink"
            @update-qty="updateQty"
            v-model:description="description"
            @create-order="createOrder"
          />
        </div>
      </div>
      <hr />
      <div class="row justify-content-center">
        <div class="col-8">
          <OrderListComponent :orderList="orderList"/>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
