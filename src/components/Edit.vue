<template>
  <div class="wrapper">
    <form class="form" @submit.prevent="onSub">
      <div class="form__group field">
        <input type="text" v-model="title"  class="form__field" autocomplete="off"  name="name" id="name" required />
        <label for="name" class="form__label">Редактирование</label>
      </div>
      <div class="form__group field">
        <input type="date" id="date" class="date__input" required v-model="date"/>
        <label for="date" class="form__label ">Дата</label>
      </div>
      <button type="submit" class="button">OK</button>
    </form>
  </div>
</template>
<script>
export default {
 props: ["editId"],
  data() {
    return {
        id:this.editId.id,
      title: this.editId.title,
      date:this.editId.date.split('.').reverse().join('-')
    };
  },
  methods: {
    onSub() {
      if (this.title.trim()) {
        const editedTodo = {
          id:this.id,
          title: this.title,
          date: this.date.split('-').reverse().join('.'),
          complited: false
        };
        this.$emit("edit-todo", editedTodo);
        this.title = "";
        this.date = "";
      }
    }
  }
};
</script>
