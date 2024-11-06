<script setup>
import { defineProps, defineEmits } from 'vue'
// props 可不用 const props = defineProps()
defineProps({
  data: Array,
})

const emit = defineEmits(['addCart'])

const addCart = item => {
  emit('addCart', item)
}
</script>

<template>
  <a
    href="#"
    class="list-group-item list-group-item-action"
    v-for="item in data"
    :key="item.id"
    @click.prevent="addCart(item)"
  >
    <div class="d-flex w-100 justify-content-between">
      <h5 class="mb-1">{{ item.name }}</h5>
      <small>${{ item.price }}</small>
    </div>
    <p class="mb-1">{{ item.description }}</p>
  </a>
</template>
