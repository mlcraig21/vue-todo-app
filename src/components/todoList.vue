<template>
  <div class="TodoList">
    <h1>Tasks Todo</h1>
    <form v-on:submit.prevent="addTodo">
      <addTodo v-model="addTodoText"/>
      <button class="btn btn btn-primary">Add</button>
    </form>
    <ul v-if="todos.length" class="todoItems">
      <todoItem v-for="todo in todos" :key="todo.id" :todo="todo" @remove="removeTodo"/>
    </ul>
    <p v-else>Nothing to do today.
      <br>hmm... You must have something to do.
      <br>Add it to the list. :)
    </p>
  </div>
</template>

<script>
import addTodo from "./addTodo.vue";
import todoItem from "./todoItem.vue";

let todoId = 1;

export default {
  components: { todoItem, addTodo },
  data() {
    return {
      addTodoText: "",
      todos: [
        {
          id: todoId++,
          text: "Add more todo items"
        },
        {
          id: todoId++,
          text: "Check off todo items"
        },
        {
          id: todoId++,
          text: "Delete these todo items"
        }
      ]
    };
  },
  methods: {
    addTodo() {
      const trimmed = this.addTodoText.trim();
      if (trimmed) {
        this.todos.push({
          id: todoId++,
          text: trimmed
        });
        this.addTodoText = "";
      }
    },
    removeTodo(idToRemove) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== idToRemove;
      });
    }
  },
  watch: {
  todos: {
    handler() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    deep: true,
   },
  },
  mounted() {
  if (localStorage.getItem('todos')) 
    this.todos = JSON.parse(localStorage.getItem('todos'));
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.TodoList {
  text-align: center;
  padding-bottom: 25px;
}
ul {
  list-style-type: none;
  padding: 0;
}
</style>
