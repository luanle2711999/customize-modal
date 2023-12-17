<template>
  <div id="app">
    <button type="button" class="btn" @click="showModal">Open Modal!</button>

    <Modal
      v-show="isModalVisible"
      @closeModal="closeModal"
      titleContent="this is a header"
      messageContent="This is a message content"
      @onOk="closeModal"
      @onCancel="closeModal"
    >
      <template v-slot:header> This is a new modal header. </template>
    </Modal>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import Modal from "./components/Modal.vue";
const isModalVisible = ref(false);
const closeModal = () => {
  isModalVisible.value = false;
};
const showModal = () => {
  isModalVisible.value = true;
};
</script>
