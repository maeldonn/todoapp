<template>
  <div id="add">
    <p v-if="copy" @click="hideMessage()">Une tâche avec ce nom existe déjà... X</p>
    <label for="newTodo">Nouveau :</label>
    <input id="newTodo" type="text" v-model="newTodo"/>
    <button @click="resetNewTodo()">Ajouter</button>
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
      copy: false,
    };
  },
  methods: {
    resetNewTodo() {
      if (String(this.newTodo).split(' ').join('') !== '') {
        if (this.click(this.newTodo)) {
          this.copy = false;
          this.newTodo = '';
        } else {
          this.copy = true;
        }
      } else {
        this.copy = false;
        this.newTodo = '';
      }
    },
    hideMessage() {
      this.copy = false;
      this.newTodo = '';
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#add {
  margin-top: 20px;
}
#add p {
  cursor: pointer;
}
#add button {
  margin: 5px;
}
</style>
