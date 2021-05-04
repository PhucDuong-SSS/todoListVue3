<template>
  <TodoItem v-for="todo in todos" v-bind:key="todo.id" :todoProps="todo" @item-complete="markCompleted" @item-delete="deleteItem" />   
  
</template>
<script>
import {ref} from 'vue'
import TodoItem from './TodoItem'
export default {
    name: 'Todos',
    components : {TodoItem},
    setup()
    {
        const todos = ref([
            {
                id: 1,
                title: 'viec1',
                isComplete: false,
        },
            {
                id: 2,
                title: 'viec2',
                isComplete: false,
        },
            {
                id: 3,
                title: 'viec3',
                isComplete: true,
        }
        ]);
        const markCompleted = id => {
            todos.value = todos.value.map(todo =>{
                if(todo.id == id) todo.isComplete = !todo.isComplete;
                return todo
            });
}
        const deleteItem = id =>{
            todos.value = todos.value.filter(todo => todo.id !== id 
            );
        }

        return {
            todos,
            markCompleted,
            deleteItem
            
        }    
    }
}
</script>

<style>

</style>