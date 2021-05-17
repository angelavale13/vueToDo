<template>
  <section class="modal" :id="name+'Modal'" tabindex="-1">
    <section class="modal-dialog">
      <section class="modal-content">
        <section class="modal-header">
          <h5 class="modal-title">{{computedTitle}}</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </section>
        <section class="modal-body">
          <label for="status">Status</label>
          <select v-model="todo.status" name="status">
            <option value="backLog">BackLog</option>
            <option value="inProgress">In Progress</option>
            <option value="complete">Complete</option>
          </select>
          <label for="title">Title</label>
          <input v-model="todo.title" name="title" type="text">
          <label for="body">Body</label>
          <input v-model="todo.body" name="body" type="text">
        </section>
        <section class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">{{type === 'Create' ? 'Cancel Create' : 'Cancel Edit'}}</button>
          <button v-if="type === 'Create'" type="button" class="btn btn-primary" @click="postOrPutTodo" data-bs-dismiss="modal">Submit</button>
          <button v-else type="button" class="btn btn-primary" @click="postOrPutTodo" data-bs-dismiss="modal">Save</button>
        </section>
      </section>
    </section>
  </section>
</template>

<script>
import axios from 'axios';
export default {
  name: 'TodoModal',
  props: {
    type: String,
    name: String,
    todo: Object,
  },
  computed: {
    computedTitle: function () {
      return this.type + ' a Todo';
    }
  },
  methods: {
    postOrPutTodo(){
      delete this.todo.createdAt;
      const id = this.todo.todoId;
      delete this.todo.todoId;
      let options = {};
       if (this.type === 'Edit') {
         console.log(this.todo);
          options = {
              url: `https://us-central1-projecttracker-c0c00.cloudfunctions.net/api/todo/${id}`,
              method: 'put',
              data: this.todo
          };
        } else {
          options = {
              url: 'https://us-central1-projecttracker-c0c00.cloudfunctions.net/api/todo',
              method: 'post',
              data: this.todo
          };
      }
      //axios sends request to api
      axios(options)
          .then(() => {
              this.$parent.currentTodo = {
                title: '',
                body: '',
                status: '',
              };
              this.$parent.fetchTodos();
          })
          .catch((error) => {
              console.log(error);
          });
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
