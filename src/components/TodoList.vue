<template>
  <div>
    <the-header @add-todo="addTodo"/>
    <div class="global-container">
      <h1>Список задач</h1>
      <p class="message-empty" v-model="todoEmpty" v-if="todoIsEmpty">Список задач пуст</p>
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
      ],
      todoIsEmpty: false
    }
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo)
      this.todoEmpty()
    },
    deleteTask(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
      this.todoEmpty()
    },
    editTask(id, title) {
      this.todos = this.todos.map(todo => {
        if (todo.id === id) {
          todo.title = title
        }
        return todo
      })
    },
    todoEmpty() {
      this.todoIsEmpty = this.todos.length === 0
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
.message-empty {
  display: flex;
  justify-content: center;
  font-size: 20px;
}
</style>