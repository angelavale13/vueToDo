<template>
  <section>
    <h3>{{todo.title}}</h3>
    <p>{{todo.body}}</p>
    <input type="button" value="View" >
    <input type="button" value="Edit" data-bs-toggle="modal" data-bs-target="#editModal" @click="editTodo">
    <input type="button" value="Delete" @click="deleteTodo">
  </section>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Todo',
  props: {
    todo: Object,
  },
  methods: {
    editTodo(){
      this.$parent.currentTodo = this.todo
    },
    deleteTodo(){
      axios
        .delete(`https://us-central1-projecttracker-c0c00.cloudfunctions.net/api/todo/${this.todo.todoId}`)
        .then(() => {
            this.$parent.fetchTodos();
        })
        .catch((err) => {
            console.log(err);
        });
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
