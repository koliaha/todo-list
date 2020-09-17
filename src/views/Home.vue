<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h1>TodoList App</h1>
    <AddForm @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all" selected>All</option>
      <option value="complet">Completed</option>
      <option value="not-complet">Not Completed</option>
    </select>
    <Loading v-if="loading" />
    <TodoList v-else-if="filterTodo.length" :todos="filterTodo" @remove-todo="removeTodo" />
    <p v-else>No Todos</p>
  </div>
</template>

<script>
import TodoList from "../components/TodoList";
import AddForm from "../components/AddForm";
import Loading from "../components/Loading";
export default {
  name: "Home",
  data() {
    return {
      todos: [
        { id: 1, title: "Play PS5", complited: false },
        { id: 2, title: "Burn PS5", complited: false },
        { id: 3, title: "Sell PS5", complited: false }
      ],
      loading: false,
      filter: 'all'
    };
  },
  mounted() {
   /*  fetch("https://jsonplaceholder.typicode.com/todos")
      .then(response => response.json())
      .then(json => {
        this.todos = json;
      }); */
  },
  components: {
    TodoList,
    AddForm,
    Loading
  },
  /* watch:{
    filter(val){
      console.log(val)
    }
  }, */
  computed:{
    filterTodo(val){
      if (this.filter === 'all'){
        return this.todos
      }
      if (this.filter === 'complet'){
        return this.todos.filter((el)=> el.complited)
      }
      if (this.filter === 'not-complet'){
        return this.todos.filter((el)=> !el.complited)
      }
      return val
    }
  },
  methods: {
    removeTodo(id) {
      console.log(id);
      setTimeout(() => {
      let todo = this.todos.filter(el => el.id != id);
        this.todos = todo;
        this.loading = false;
      }, 1000);
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    }
  }
};
</script>
