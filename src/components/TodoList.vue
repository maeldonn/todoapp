<template>
  <div>
    <h1>Ma TodoList</h1>
    <div v-for="item in todos" :key="item.name" class="list">
      <Todo
        :name="item.name"
        :completed="item.completed"
        :toggle="() => toggleTodo(item)"
        :remove="() => removeTodo(item)"
      />
    </div>
    <TodoAdd :click="addTodo" />
  </div>
</template>

<script>
import Todo from './Todo.vue';
import TodoAdd from './TodoAdd.vue';

export default {
  name: 'TodoList',
  components: {
    Todo,
    TodoAdd,
  },
  props: {
    name: String,
    completed: Boolean,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    toggleTodo(todo) {
      const position = this.todos.indexOf(todo);
      if (position !== -1) {
        this.todos[position].completed = !this.todos[position].completed;
      }
    },
    removeTodo(todo) {
      const position = this.todos.indexOf(todo);
      if (position !== -1) {
        this.todos.splice(position, 1);
      }
    },
    isAcopy(todoName) {
      let copy;
      this.todos.forEach((todo) => {
        if (String(todo.name).toLowerCase() === String(todoName).toLowerCase()) {
          copy = true;
        }
      });
      if (copy) {
        return true;
      }
      return false;
    },
    addTodo(newTodoName) {
      if (newTodoName !== '') {
        if (!this.isAcopy(newTodoName)) {
          this.todos.push({ name: newTodoName, completed: false });
          return true;
        }
      }
      return false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.list {
  display: block;
  user-select: none;
}

h1 {
  font-size: 3rem;
}
</style>
