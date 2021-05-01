<template>
  <section>
    <h3>{{title}}</h3>
    <p>{{body}}</p>
    <input type="button" value="View">
    <input type="button" value="Edit">
    <input type="button" value="Delete">
  </section>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    title: String,
    body: String,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
