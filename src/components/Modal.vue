<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div
        class="modal"
        :style="{ height: `${height}px`, width: `${width}px` }"
      >
        <header class="modal-header">
          <slot name="header"> {{ titleContent }} </slot>
          <button type="button" class="btn-close" @click="close">x</button>
        </header>

        <section class="modal-body">
          <slot name="body"> {{ messageContent }} </slot>
        </section>

        <footer class="modal-footer">
          <div class="group-btn">
            <slot name="footer">
              <button type="button" class="btn-function" @click="okFunction">
                {{ okText }}
              </button>
              <button
                type="button"
                class="btn-function"
                @click="cancelFunction"
              >
                {{ cancelText }}
              </button>
            </slot>
          </div>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script setup lang="ts">
defineProps({
  messageContent: {
    type: String,
    default: "",
    required: false,
  },
  titleContent: {
    type: String,
    default: "",
    required: false,
  },
  width: {
    type: Number,
    default: 600,
    required: false,
  },
  height: {
    type: Number,
    default: 300,
    required: false,
  },
  cancelText: {
    type: String,
    default: "Cancel",
    required: false,
  },
  okText: {
    type: String,
    default: "OK",
    required: false,
  },
});
const emit = defineEmits(["closeModal", "onCancel", "onOk"]);
const close = () => {
  emit("closeModal");
};

const okFunction = () => {
  emit("onOk");
};

const cancelFunction = () => {
  emit("onCancel");
};
</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  color: #000;
  justify-content: space-between;
  height: 15%;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
  justify-content: flex-end;
  height: 15%;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
  height: 70%;
}

.group-btn {
  display: flex;
  text-align: right;
  justify-content: right;
  align-items: center;
  bottom: 0;
}
.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color: #000;
  background: transparent;
}

.btn-function {
  margin-right: 8px;
  border: 1px solid #000;
  border-radius: 2px;
  color: #000;
}
.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.5s ease;
}
</style>
