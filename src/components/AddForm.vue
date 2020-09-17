<template>
  <div>
    <form :class="$style.form" @submit.prevent="onSub">
      <input type="text" :class="$style.input" v-model="title" />
      <button type="submit">Create</button>
    </form>
  </div>
</template>
<script>
export default {
    data(){
        return{
            title:''
        }
    },
    methods:{
        onSub(){
            console.log('hey', this.title)
            if(this.title.trim()){
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    complited: false
                }
                this.$emit('add-todo', newTodo)
                this.title=''
            }
        }
    }
};
</script>
<style  module>
.form {
  display: flex;
  justify-content: center;
}
.input {
  width: 400px;
}
</style>