<template>
  <div id="app">
    <Header />
    <section class="todolist">
      <TodoAdd :click="addTodo" />
      <div class="list">
        <span v-for="item in todos" :key="item.name">
          <Todo
            :name="item.name"
            :completed="item.completed"
            :toggle="() => toggleTodo(item)"
            :remove="() => removeTodo(item)"
          />
        </span>
      </div>
      <div v-if="todos.length !== 0" class="remove-all">
        <button class="remove" @click="removeAll">REMOVE ALL</button>
      </div>
    </section>
    <Footer />
  </div>
</template>
<script>
import Todo from './components/Todo.vue';
import TodoAdd from './components/TodoAdd.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    Todo,
    TodoAdd,
    Header,
    Footer,
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
        if (
          String(todo.name).toLowerCase() === String(todoName).toLowerCase()
        ) {
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
    removeAll() {
      this.todos = [];
    },
  },
};
</script>

<style>
body,
html {
  padding: 0;
  margin: 0;
}

body {
  width: 100vw;
  height: 100vh;
  background: #ff7b73;
}

::-moz-selection {
  color: #ff7b73;
  background: #ffffffff;
}

::selection {
  color: #ff7b73;
  background: #ffffffff;
}

#app {
  height: 100%;
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  -webkit-box-pack: justify;
      -ms-flex-pack: justify;
          justify-content: space-between;
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
  color: #ffffff;
}

.todolist {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  -webkit-box-pack: justify;
      -ms-flex-pack: justify;
          justify-content: space-between;
  height: 80%;
}

.list {
  margin: 0 2rem;
  height: 40vh;
  overflow: scroll;
  max-width: 100%;
}

.remove-all {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
      -ms-flex-pack: center;
          justify-content: center;
}

.remove {
  cursor: pointer;
  border: none;
  border-radius: 80px;
  background: #ffffff;
  font-size: 1.5rem;
  color: #ff7b73;
  padding: 10px 15px;
  -webkit-transition: color 0.5s ease-in-out;
  -o-transition: color 0.5s ease-in-out;
  transition: color 0.5s ease-in-out;
}

.remove:hover {
  background: #ff7b73;
  color: #ffffff;
}
</style>
