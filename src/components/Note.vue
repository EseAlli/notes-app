<template>
  <div class="hello">
    <p>Grocericies</p>
    <p>Milk, Coffee, cookies</p>
    <p>17/07/2023</p>
  </div>
</template>

<script>
export default {
  name: "NoteItem",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
