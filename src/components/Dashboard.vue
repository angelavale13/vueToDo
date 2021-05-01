<template>
  <main>
    <h1>Project Tracker</h1>
    <section>
      <h2>About this web app</h2>
        <p>Made with Vue JS, Bootstrap, Firebase</p>
    </section>
    <article>
      <section>
        <h3>BackLog</h3>
        <Todo v-for="todo in backLog" :title="todo.title" :body="todo.body" :key="todo.id"/>
      </section>
      <section>
        <h3>In Progress</h3>
        <Todo v-for="todo in inProgress" :title="todo.title" :body="todo.body" :key="todo.id"/>
      </section>
      <section>
        <h3>Complete</h3>
        <Todo v-for="todo in complete" :title="todo.title" :body="todo.body" :key="todo.id"/>
      </section>
    </article>
  </main>
</template>

<script>
import Todo from './Todo.vue'

export default {
  name: 'Dashboard',
  components: {
    Todo,
  },
  data() {
    return {
      todos: [
        {
          "todoId": "pTa4Rqw6wN3EqG4vgfkK",
          "title": "Hello World",
          "body": "456",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:13.848Z"
        },
        {
          "todoId": "HajfPdb80fkSMkWzZfRa",
          "title": "Hello World",
          "body": "123",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:07.652Z"
        },
      ],
      backLog: [{
          "todoId": "pTa4Rqw6wN3EqG4vgfkK",
          "title": "Hello World",
          "body": "something",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:13.848Z"
        },
        {
          "todoId": "HajfPdb80fkSMkWzZfRa",
          "title": "Hello World",
          "body": "else",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:07.652Z"
        },],
      inProgress: [
        {
          "todoId": "pTa4Rqw6wN3EqG4vgfkK",
          "title": "Hello World",
          "body": "in progro",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:13.848Z"
        },
        {
          "todoId": "HajfPdb80fkSMkWzZfRa",
          "title": "Hello World",
          "body": "yaya",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:07.652Z"
        },
      ],
      complete: [
        {
          "todoId": "pTa4Rqw6wN3EqG4vgfkK",
          "title": "Hello World",
          "body": "completed here",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:13.848Z"
        },
        {
          "todoId": "HajfPdb80fkSMkWzZfRa",
          "title": "Hello World",
          "body": "nono",
          "status": "complete",
          "createdAt": "2021-05-01T20:15:07.652Z"
        },
      ],
      title: '',
      body: '',
      status: '',
      todoId: '',
      errors: [],
      open: false,
      uiLoading: true,
      buttonType: '',
      viewOpen: false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
