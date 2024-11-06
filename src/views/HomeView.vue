<script setup>
import { ref } from 'vue'
import HeaderComponent from '../components/HeaderComponent.vue'
import CardComponent from '../components/CardComponent.vue'
import FooterComponent from '../components/FooterComponent.vue'

const data = ref([
  {
    title: '標題1',
    content: `Some quick example text to build on the card title and make up the
          bulk of the card's content.`,
    imgUrl:
      'https://images.unsplash.com/photo-1555036803-4b8b34490116?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fGNhdCUyMHRveXxlbnwwfHwwfHx8MA%3D%3D',
  },
  {
    title: '標題2',
    content: `Some quick example text to build on the card title and make up the
          bulk of the card's content.`,
    imgUrl:
      'https://images.unsplash.com/photo-1555036803-4b8b34490116?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fGNhdCUyMHRveXxlbnwwfHwwfHx8MA%3D%3D',
  },
  {
    title: '標題3',
    content: `Some quick example text to build on the card title and make up the
          bulk of the card's content.`,
    imgUrl:
      'https://images.unsplash.com/photo-1555036803-4b8b34490116?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fGNhdCUyMHRveXxlbnwwfHwwfHx8MA%3D%3D',
  },
  {
    title: '標題4',
    content: `Some quick example text to build on the card title and make up the
          bulk of the card's content.`,
    imgUrl:
      'https://images.unsplash.com/photo-1555036803-4b8b34490116?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fGNhdCUyMHRveXxlbnwwfHwwfHx8MA%3D%3D',
  },
])


const value = ref('這是外層單向數據流的文字')

const editTitle = (newTitle, index) => { 
  console.log('editTitle', newTitle) 
  // 修改正確的索引值 
  data.value[index].title = newTitle 
}
const card = ref('這是外層 card的文字')

const addCard = (cardTitle) => {
  console.log('addCard',cardTitle);
}
</script>

<template>
  <div class="container">
    <HeaderComponent />
    <div class="body">
      <div class="row g-3">
        <!--實作通常會同名，HTML屬性一律是小寫，物件屬性一律用小駝峰 -->
        <!-- 外到內：props，前內後外，前面是內部名稱，後面是外部的值 -->
        <!-- 內到外：emit，前內後外，前面是內部觸發的事件，後面是外部觸發的函式 -->
        <CardComponent
          :inner-data="data"
          :value="value"
          @emit-title="editTitle"
        />
      </div>
      <CardComponent :card="card" @add-card="addCard" />
    </div>
    <FooterComponent />
  </div>
</template>
