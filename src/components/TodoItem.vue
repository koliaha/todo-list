<template>
    <div :class="$style.wrap">
        <span :class="{[$style.done]: todo.complited}">
            <input type="checkbox" name="" id="" @change="todo.complited = !todo.complited">
            <strong :class="$style.title">{{todo.title | uppercase}}</strong>
        </span>
        <button :class="$style.delBtn" @click="$emit('remove-todo', todo.id)">&times;</button>
    </div>
</template>

<script>
export default {
    props:{
        todo:{
            type: Object,
            required: true
        }
    },
    filters:{
        uppercase(value){
            return value.toUpperCase()
        }
    }
}
</script>

<style module>
    .wrap{
        width: 600px;
        margin: 15px auto;
        padding: 10px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border: 1px solid gray;
        text-align: center;
    }
    .title{
        font-size: 25px;
    }
    .delBtn{
        background-color: red;
        border-radius: 50%;
        color: white;
        border: none;
        cursor: pointer;
        width: 50px;
        height: 50px;
        font-size: 25px;
        outline: none;
        font-weight: bold;
    }
    .done{
        text-decoration: line-through;
    }
</style>