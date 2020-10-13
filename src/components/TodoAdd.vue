<template>
  <div class="form">
    <div v-if="errorMessage" class="error">{{ errorMessage }}</div>
    <form @submit.prevent="addNewTodo()">
      <input
        id="newTodo"
        type="text"
        v-model="newTodo"
        placeholder="enter a todo title"
        maxlength="80"
      />
      <button>ADD</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'TodoAdd',
  props: {
    click: Function,
  },
  data() {
    return {
      newTodo: '',
      errorMessage: '',
    };
  },
  watch: {
    newTodo: {
      handler() {
        this.errorMessage = '';
      },
    },
  },
  methods: {
    addNewTodo() {
      if (String(this.newTodo).split(' ').join('') !== '') {
        if (this.click(this.newTodo)) {
          this.newTodo = '';
        } else {
          this.errorMessage = 'A task with this name is already existing...';
        }
      } else {
        this.newTodo = '';
      }
    },
  },
};
</script>

<style scoped>
.form {
  max-width: 100%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;

  flex-direction: column;

  justify-content: center;

  align-items: center;
}

form {
  height: 5em;
  display: flex;
  align-items: center;
  border-radius: 1000px;
  background: #ffffff;
}

input {
  height: 100%;
  background: none;
  border: none;
  font-size: 1.5rem;
  color: #ff7b73;
  text-align: center;
  margin: 0 10px 0 20px;
}

input::-moz-selection {
  color: #ffffffff;
  background: #ff7b73;
}

input::selection {
  color: #ffffffff;
  background: #ff7b73;
}

input::placeholder {
  opacity: 0.7;
}

input:focus {
  outline: none;
}

button {
  cursor: pointer;
  border: none;
  border-radius: 80px;
  background: #ff7b73;
  font-size: 1.5rem;
  color: inherit;
  padding: 10px 20px;
  margin-right: 15px;
}

.error {
  margin: 0 2rem 1rem 2rem;
  max-width: 100%;
  font-size: 1.4em;
  font-family: inherit;
  color: #ffffff;
  text-align: center;
}

@media only screen and (max-width: 470px) {
form {
  height: 4em;
}

input {
  font-size: 1.2rem;
  margin: 0 5px 0 10px;
}

button {
  font-size: 1.2rem;
  padding: 5px 10px;
  margin-right: 10px;
}

.error {
  margin: 0 2rem 1rem 2rem;
  font-size: 1.2em;
}
}
</style>
