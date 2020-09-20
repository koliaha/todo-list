<template>
  <div id="app">
    <img class="logo" alt="Vue logo" src="./assets/sticker.svg" />
    <h1 class="title_text">Список задач</h1>
    <div class="wrapper">
      <AddForm @add-todo="addTodo" />
      <div class="search_filter">
        <input type="text" v-model="search" class="panel search_input" placeholder="Найти..." />
        <select class="panel selecter" v-model="filter" >
          <option value="all" selected>Все</option>
          <option value="complet">Завершены</option>
          <option value="not-complet">Не завершены</option>
        </select>
      </div>
      <Edit v-if="editing" @edit-todo="editedTodo" :editId="editId" />
      <Loading v-else-if="loading"/>
      <TodoList
        v-else-if="filterTodo.length"
        :todos="filterTodo"
        @remove-todo="removeTodo"
        @edit-todo="editTodo"
      />
      <p class="title_text" v-else>Задачи отсутсвуют</p>
    </div>
  </div>
</template>
<script>
import TodoList from "./components/TodoList";
import AddForm from "./components/AddForm";
import Loading from "./components/Loading";
import Edit from "./components/Edit";
export default {
  name: "Home",
  data() {
    return {
      todos: [
        { id: 1, title: "Купить хлеб", date: "12.09.2020", complited: false },
        { id: 2, title: "Купить PS5", date: "14.10.2020", complited: false },
        {
          id: 3,
          title: "Продать Ferarri",
          date: "11.11.2020",
          complited: false
        }
      ],
      loading: false,
      filter: "all",
      search: "",
      editId: null,
      editing: false
    };
  },
  mounted() {},
  components: {
    TodoList,
    AddForm,
    Loading,
    Edit
  },

  computed: {
    filterTodo(val) {
      const searched = this.todos.filter(post => {
        return post.title.toLowerCase().includes(this.search.toLowerCase());
      });
      console.log(searched)
      if (this.filter === "all") {
        return searched;
      }
      if (this.filter === "complet") {
        return searched.filter(el => el.complited);
      }
      if (this.filter === "not-complet") {
        return searched.filter(el => !el.complited);
      }
      return val
    }
  },
  methods: {
    removeTodo(id) {
      let todo = this.todos.filter(el => el.id != id);
      this.todos = todo;
      this.loading = false;
    },
    editTodo(id) {
      console.log(id);
      this.editing = true;
      this.editId = this.todos.find(el => el.id == id);
    },
    editedTodo(eT) {
      const id = eT.id;
      this.todos.map(el => {
        if (el.id == id) {
          el.title = eT.title;
          el.date = eT.date;
        }
      });
      this.editing = false;
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    searchField() {
      console.log(this.search);
    }
  }
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: rgb(34, 193, 195);
  background: linear-gradient(
    0deg,
    rgba(34, 193, 195, 1) 0%,
    rgba(167, 45, 253, 1) 100%
  );
  min-height: 100vh;
  box-sizing: border-box;
}

.wrapper {
  max-width: 600px;
  width: 100%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.logo {
  width: 150px;
}
.title_text {
  color: #fff;
  text-transform: uppercase;
  font-size: 35px;
  border-radius: 10px;
}

.search_filter {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  .panel {
    margin: 20px;
    width: 50%;
    height: 50px;
    font-size: 25px;
    padding: 10px;
    outline: none;
  }
  .selecter {
    cursor: pointer;
    color: #fff;
    background-color: rgb(247, 165, 12);
  }
  .search_input {
    color: #000;
  }
}
@media screen  and (max-width: 450px){
  .wrapper {
  max-width: 95%;
  }
   .search_filter{
    flex-direction: column;
  }
  .search_filter .panel{
    width: 100%;
  }
}
</style>
