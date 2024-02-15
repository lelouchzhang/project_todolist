<template>
  <ul class="todo-main">
    <ItemItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      :updateTodo="updateTodo"
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
import ItemItem from './ItemItem.vue'
export default {
  name: 'ItemsItems',
  components: {
    ItemItem,
  },
  props: ['todos', 'updateTodo', 'deleteTodo'],
}
</script>

<style scoped>
/*list*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
