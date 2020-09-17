<template>
    <div>
         <ul :class="$style.listStyle">
            <TodoItem
                v-for="todo of todos"
                :todo="todo"
                :key="todo.id"
                @remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from './TodoItem'
export default {
    props:['todos'],
    components:{
        TodoItem
    },
    methods:{
        removeTodo(id){
            this.$emit('remove-todo', id)
        }
    }
}
</script>

<style module>
    .listStyle{
        list-style: none;
    }
</style>