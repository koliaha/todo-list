<template>
  <div>
    <div class="wrap" >
      <span :class="{done: todo.complited}">
        <input type="checkbox" name id @change="todo.complited = !todo.complited" />
        <strong class="title" @click="todo.complited = !todo.complited">{{todo.title | uppercase}}</strong>
        <strong class="date">{{todo.date}}</strong>
      </span>
      <div class="btn__group">
        <button class="btn editBtn" @click="$emit('edit-todo', todo.id)">-</button>
        <button class="btn delBtn" @click="$emit('remove-todo', todo.id)">&times;</button>
      </div>
    </div>
   
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase();
    }
  }
};
</script>

<style lang="scss" scope>
* {
  box-sizing: border-box;
}
.wrap {
  width: 100%;
  margin: 15px auto;
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 1px solid gray;
  text-align: center;
  background-color: #fff;
  border-radius: 10px;
}
.title {
  font-size: 25px;
  line-height: 25px;
  margin: 0 20px;
  cursor: pointer;
}
.date {
  font-size: 17px;
  line-height: 25px;
  color: rgb(143, 143, 143);
}
.delBtn {
  background-color: red;
}
.editBtn {
  background-color: rgb(3, 180, 106);
}
.btn {
  margin: 0 5px;
  border-radius: 50%;
  color: white;
  border: none;
  cursor: pointer;
  width: 50px;
  height: 50px;
  font-size: 20px;
  outline: none;
  font-weight: bold;
  transition: 0.3s;
  &:hover {
    opacity: 0.7;
  }
}
.done {
  text-decoration: line-through;
  opacity: 0.7;
}
.wrap {
  &:hover .title {
    color: cadetblue;
  }
}
@media screen  and (max-width: 450px){
  .wrap {
      flex-direction: column;
  }
  .title, .date {
    font-size: 15px;
}
.btn {
  margin: 5px 5px;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  font-size: 15px;
} 
}
</style>