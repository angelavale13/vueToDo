<template>
  <main>
    <h1 class="text-primary">Project Tracker</h1>
    <section>
      <h4>About this web app</h4>
        <p>Made with Vue JS, Bootstrap, Firebase</p>
    </section>
    <article>
      <section>
        <h6>BackLog</h6>
        <Todo v-for="todo in backLog" :todo="todo" :key="todo.id"/>
      </section>
      <section>
        <h6>In Progress</h6>
        <Todo v-for="todo in inProgress" :todo="todo" :key="todo.id"/>
      </section>
      <section >
        <h6>Complete</h6>
        <Todo v-for="todo in complete" :todo="todo" :key="todo.id"/>
      </section>
    </article>
    <input type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#createModal" value="New Task" @click="createTodo">
    <TodoModal type="Create" name="create" :todo="currentTodo"/>
    <TodoModal type="Edit" name="edit" :todo="currentTodo"/>
  </main>
</template>

<script>
import Todo from './Todo.vue'
import TodoModal from './TodoModal.vue'
import axios from 'axios'

export default {
  name: 'Dashboard',
  components: {
    Todo,
    TodoModal,
  },
  data() {
    return {
      // todos: [
      //   {
      //     "todoId": "pTa4Rqw6wN3EqG4vgfkK",
      //     "title": "Hello World",
      //     "body": "456",
      //     "status": "complete",
      //     "createdAt": "2021-05-01T20:15:13.848Z"
      //   },
      //   {
      //     "todoId": "HajfPdb80fkSMkWzZfRa",
      //     "title": "Hello World",
      //     "body": "123",
      //     "status": "complete",
      //     "createdAt": "2021-05-01T20:15:07.652Z"
      //   },
      // ],
      backLog: [],
      inProgress: [],
      complete: [],
      currentTodo: {
        title: '',
        body: '',
        status: '',
      },
      errors: [],
      open: false,
      uiLoading: true,
      buttonType: '',
      viewOpen: false
    }
  },
  mounted: function () {
    this.$nextTick(function () {
      this.fetchTodos();
    })
  },
  methods: {
    fetchTodos(){
      axios
        .get('https://us-central1-projecttracker-c0c00.cloudfunctions.net/api/todos')
        .then((response) => {
                this.backLog = response.data.filter((todo) => 
                todo.status === "backLog");
                this.inProgress = response.data.filter((todo) => 
                todo.status === "inProgress");
                this.complete = response.data.filter((todo) => 
                todo.status === "complete");
                this.uiLoading = false;
        })
        .catch((err) => {
            console.log(err);
        });
    },
    createTodo(){
      this.currentTodo.title = "";
      this.currentTodo.body = "";
      this.currentTodo.status = "backLog";

    },
    
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
