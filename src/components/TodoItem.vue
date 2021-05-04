<template>
  <p :class="['todo-item', todoProps.isComplete ?'isCompleted':'']">  <input type="checkbox" :checked="todoProps.isComplete" v-on:change="markCompleted"/>
    {{todoProps.title}}
    <button class="del-btn" @click="deleteTodo">Delete</button>
    </p>
</template>

<script>
export default {
    name: 'TodoItem',
    props: ['todoProps'],
    setup(props, content){
    const markCompleted = ()=>{
        content.emit('item-complete', props.todoProps.id)
    };
    const deleteTodo = ()=>{
        content.emit('item-delete', props.todoProps.id)
    }
    return {
    markCompleted ,
    deleteTodo

    }

}
}

</script>

<style>
    .del-btn{
        background: #ff0000;
        color: #fff;
        border: none;
        cursor: pointer;
        float: right;
    }
    .todo-item{
        background: #f4f4f4;
        padding: 10px;
        margin: 0;
        border: 1px #ccc dotted;    
    }
    .isCompleted {
       text-decoration: line-through; 
        }
</style>