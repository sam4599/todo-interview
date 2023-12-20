<template>
  <div>
    <the-header @add-todo="addTodo"/>
    <div class="global-container">
      <h1>Список задач</h1>
      <li class="todo-item">
        <todo-item
          v-for="todo of todos"
          :todo="todo"
          @delete-task="deleteTask"
          @edit-task="editTask"
        />
      </li>
    </div>
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader.vue";
import TodoItem from "@/components/TodoItem.vue";


export default {
  name: 'TodoList',
  components: {
    TheHeader,
    TodoItem
  },
  data() {
    return {
      todos: [
        {id: 1, title: 'Печеники'},
        {id: 2, title: 'Чай'},
        {id: 3, title: 'Сыр'}
      ]
    }
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo)
    },
    deleteTask(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    editTask(id, title) {
      this.todos = this.todos.map(todo => {
        if (todo.id === id) {
          todo.title = title
        }
        return todo
      })
    }
  }
}
</script>

<style scoped>
h1 {
  margin: 112px 0 52px;
}
.todo-item {
  display: flex;
  flex-wrap: wrap;
  gap: 50px;
}
</style>