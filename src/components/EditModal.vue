<template>
<div>
  <span @click="showModal = true" class="pensil"><pensil-svg/></span>
  <div v-if="showModal" class="modal">
    <div class="modal-content">
      <div class="modal-content-top">
        <p>[Редактирование]</p>
        <span class="close" @click="closeModal">&times;</span>
      </div>
      <form class="form" @keydown.enter.prevent>
        <p>Название</p>
        <input type="text" v-model="currentTitle" @input="isTitleEmpty = false" :class="{ 'input-error': isTitleEmpty, 'input-shake': isTitleEmpty }">
        <p v-if="isTitleEmpty" class="error-message">название обязательное поле</p>
        <div class="button-modal">
          <button class="button-delete" @click="deleteTask">Удалить</button>
          <button class="button-edit" @click="editTask" :disabled="isTitleEmpty">Изменить</button>
        </div>
      </form>
    </div>
  </div>
</div>
</template>

<script>
import PensilSvg from "@/assets/svg/PensilSvg.vue";

export default {
  name: 'EditModal',
  components: {
    PensilSvg,
  },
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showModal: false,
      title: '',
      currentTitle: '',
      isTitleEmpty: false
    }
  },
  created() {
    this.currentTitle = this.todo.title
  },
  methods: {
    clearInput() {
      this.title = ''
    },
    closeModal() {
      this.showModal = false
      this.clearInput()
      this.isTitleEmpty = false
    },
    deleteTask() {
      this.$emit('delete-task', this.todo.id)
      this.showModal = false
    },
    editTask() {
      if (this.currentTitle.trim() !== '') {
        if (this.currentTitle.trim() !== this.todo.title.trim()) {
          this.$emit('edit-task', this.currentTitle, this.todo.id)
          this.showModal = false
        }
        else {
          this.isTitleEmpty = true
        }
      } else {
        this.isTitleEmpty = true
      }
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
  color: #F4C959;
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
  display: flex;
  justify-content: end;
  gap: 8px;
  margin-top: 24px;
}
.button-edit {
  padding: 10px 20px;
  background: #008180;
  color: #FFFFFF;
  border: none;
}
.button-delete {
  padding: 10px 20px;
  background: #FC5151;
  color: #FFFFFF;
  border: none;
}
.pensil {
  display: flex;
  border: 2px solid #F4C959;
  width: 90px;
  height: 90px;
  justify-content: center;
  align-items: center;
  border-bottom-right-radius: 16px;
  border-top-right-radius: 16px;
  background: #f1f1f1;
  cursor: pointer;
}
.pensil:hover {
  border: 2px solid rgba(224, 182, 58, 0.98);
  background: #f5f5f5;
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