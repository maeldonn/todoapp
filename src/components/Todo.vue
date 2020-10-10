<template>
  <div class="todo">
    <span @click="remove">❌</span>
    <h1 @click="toggle" :class="completed ? 'is-completed' : null">{{name}}</h1>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    name: { type: String, required: true },
    completed: { type: Boolean, required: true },
    toggle: { type: Function, required: true },
    remove: { type: Function, required: true },
  },
};
</script>

<style scoped>
.todo {
  margin: 20px;
}

h1, span {
  cursor: pointer;
  display: inline;
  font-size: 2em;
}

span {
  margin-right: 30px;
}

h1 {
  text-align: center;
}

.is-completed {
  text-decoration: line-through;
}
</style>
