<template>
  <div>
    <app-button @click="showModal = true"/>
    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <div class="modal-content-top">
          <p>[Создание]</p>
          <span class="close" @click="closeModal">&times;</span>
        </div>
        <form class="form" @submit.prevent="onSubmit">
          <p>Название</p>
          <input type="text" placeholder="Задача на сегодня" v-model="title" @input="isTitleEmpty = false" :class="{'input-error': isTitleEmpty, 'input-shake': isTitleEmpty}">
          <p v-if="isTitleEmpty" class="error-message">название обязательное поле</p>
          <button class="button-modal">Создать</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import AppButton from "@/components/ui/AppButton.vue";

export default {
  name: 'CreateModal',
  components: {
    AppButton
  },
  data() {
    return {
      showModal: false,
      title: '',
      isTitleEmpty: false
    }
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title
        }
        this.$emit('send-todo', newTodo)
        this.closeModal()
      } else {
        this.isTitleEmpty = true
      }
    },
    clearInput() {
      this.title = ''
    },
    closeModal() {
      this.showModal = false
      this.clearInput()
      this.isTitleEmpty = false
    }
  }
}
</script>

<style scoped>
.modal {
  display: block;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}
.modal-content-top {
  display: flex;
  justify-content: space-between;
}
.modal-content-top > p {
  color: #008180;
  margin-top: 24px;
  font-size: 20px;
}
.form {
  margin-top: 32px;
}
.form > p {
  font-size: 16px;
}
.form input {
  width: 462px;
  height: 46px;
  text-indent: 12px;
  margin-top: 4px;
}
.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 502px;
  height: 244px;
  border-radius: 16px;
}
.close {
  font-size: 28px;
  font-weight: bold;
  cursor: pointer;
  color: #FC5151;
  width: 16px;
  height: 16px;
}
.close:hover,
.close:focus {
  color: black;
  cursor: pointer;
}
.button-modal {
  padding: 10px 20px;
  background: #008180;
  color: #FFFFFF;
  border: none;
  margin-top: 24px;
  float: right;
}
.input-error {
  border: 2px solid #ffc8ce;
}
@keyframes shake{
  0% { transform: translateX(-2px)}
  20% { transform: translateX(2px)}
  40% { transform: translateX(-2px)}
  60% { transform: translateX(2px)}
  80% { transform: translateX(-2px)}
  100% { transform: translateX(0)}
}
.input-shake {
  animation: shake 0.4s ease-in-out;
}
.error-message {
  position: absolute;
  color: #FC5151;
  z-index: 1;
  margin-left: 8px;
}
</style>