<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue'
import axios from 'axios'

const inputTel = ref('')
const errors = ref([])
const errorValidate = ref(true)

const Validate = () => {
  if (inputTel.value.length <= 1) {
    errorValidate.value = false
  } else {
    PostTel
  }
}


const PostTel = () => {
  axios.post('http://localhost:3001/telephones', inputTel)
  .then((response) => {
    console.log(response);
    inputTel.value = ''
  })
  .catch((error) => {
    console.log(error);
  }),
  setTimeout(() => alert('вы отправили номер телефона дождитесь ответа'), 3000)
}
</script>

<template>
  <header class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
      <form 
      method="post" 
      @submit.prevent="Validate" 
      class=" w-full flex" 
      action="#">
            <div id="search"><input v-model="inputTel" class=""  placeholder="Номер телефона ..." type="number"></div>
          <div id="search1"><button type="submit">Заказать</button></div>
      </form>
      <div class="text-xl text-center text-red-500" v-if="errorValidate == false">Укажите номер</div>
  </header>
  <RouterView />
</template>

<style scoped>



</style>

