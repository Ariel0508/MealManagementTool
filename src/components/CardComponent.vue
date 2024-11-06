<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps(['innerData', 'value', 'card'])
console.log(props)
const emit = defineEmits(['emitTitle', 'addCard']) // 定義事件名稱
// emit方法一
const emitTitle = (newTitle, index) => {
  console.log('內層觸發了 emit')
  emit('emitTitle', newTitle, index) // 傳遞事件名稱和參數
}
const cardTitle = (newTitle, index) => {
  console.log('內層觸發了 cardTitle')
  emit('addCard', newTitle, index) // 傳遞事件名稱和參數
}
</script>

<template>
  <div class="col-4" v-for="(item, index) in innerData" :key="item.title">
    <div class="card">
      <img :src="item.imgUrl" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5 class="card-title">{{ item.title }}</h5>
        <p class="card-text">
          {{ item.content }}
        </p>
        <!-- 會出錯，因為單向數據流，內層不能改外層資料 -->
        <!-- <input type="text" v-model="value"> -->
        <input
          type="text"
          v-model="item.title"
          @input="emitTitle(item.title, index)"
        />
        <a
          href="#"
          class="btn btn-primary"
          @click="emitTitle(item.title, index)"
          >Go somewhere</a
        >
        <!-- emit方法二 -->
        <a
          href="#"
          class="btn btn-primary"
          @click.prevent="emitTitle('這是內層傳遞的文字', index)"
          >傳遞事件</a
        >
        <a href="#" class="btn btn-primary" @click.prevent="cardTitle(card)"
          >cardTitle</a
        >
      </div>
    </div>
  </div>
</template>
