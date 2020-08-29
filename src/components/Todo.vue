<template>
  <div class="todo">
    <p @click="remove">❌</p>
    <h1>{{name}}</h1>
    <p v-if="completed" @click="toggle">[✅]</p>
    <p v-else @click="toggle">[ ]</p>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    name: String,
    completed: Boolean,
    toggle: Function,
    remove: Function,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.todo * {
  display: inline;
  padding: 10px;
}

.todo p {
  cursor: pointer;
}

</style>
