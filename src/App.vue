<script setup lang="ts">
import { ref } from 'vue';
import BaseModal from './components/BaseModal.vue';

const show1 = ref(false)
const show2 = ref(false)
</script>

<template>
  <button @click="show1 = true">show modal 1</button>
  <BaseModal :show="show1" @close="show1 = false">
    <button @click="show2 = true">show modal 2</button>
    <BaseModal :show="show2" @close="show2 = false" @backdrop="show1 = false; show2 = false">
      <input type="text">
    </BaseModal>
    <div class="box">
      <div class="test"></div>
    </div>
  </BaseModal>
</template>

<style lang="scss">
* {
  box-sizing: border-box;
  font-family: sans-serif;
  margin: 0;
}
.box {
  background-color: lightgray;
  height: 50px;
  position: relative;

  .test {
    position: absolute;
    width: 50px;
    height: 200px;
    background-color: red;
  }
}
.footer {
  display: flex;
  justify-content: space-between;
}
</style>
