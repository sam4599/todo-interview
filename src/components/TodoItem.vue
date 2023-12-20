<template>
    <div class="item-component">
      {{ todo.title }}
      <edit-modal
        :todo="todo"
        @edit-task="editTask"
        @delete-task="deleteTask"
      />
    </div>
</template>

<script>
import PensilSvg from "@/assets/svg/PensilSvg.vue";
import EditModal from "@/components/EditModal.vue";

export default {
  name: 'TodoItem',
  components: {
    PensilSvg,
    EditModal
  },
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteTask(id) {
      this.$emit('delete-task', id)
    },
    editTask(id, title) {
      this.$emit('edit-task', title, id)
    }
  }
}
</script>

<style scoped>
.item-component {
  display: flex;
  flex-basis: 30%;
  height: 90px;
  border-radius: 16px;
  align-items: center;
  justify-content: space-between;
  background: #FFFFFF;
  padding-left: 24px;
  font-size: 20px;
}
</style>