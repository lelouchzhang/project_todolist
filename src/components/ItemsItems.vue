<template>
  <ul class="todo-main">
    <transition-group appear name="todo">
      <ItemItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
      />
    </transition-group>
  </ul>
</template>

<script>
import ItemItem from './ItemItem.vue'
export default {
  name: 'ItemsItems',
  components: {
    ItemItem,
  },
  props: ['todos'],
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
/* todo list animated */
@keyframes todoAni {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0%);
  }
}
.todo-enter-active {
  animation: todoAni 0.5s ease-in-out;
}
.todo-leave-active {
  animation: todoAni 0.2s ease-in-out reverse;
}
</style>
