<template>
    <AddTodo @addItem="addTodo"/>

  <TodoItem v-for="todo in todos" v-bind:key="todo.id" :todoProps="todo" 
  @item-complete="markCompleted" 
  
  @item-delete="deleteItem" />   
  
</template>
<script>
import {ref} from 'vue';
import TodoItem from './TodoItem';
import AddTodo from './AddTodo';
import {v4 as uuidv4} from 'uuid'

export default {
    name: 'Todos',
    components : {TodoItem, AddTodo},
    setup()
    {
        const todos = ref([
            {
                id: uuidv4(),
                title: 'viec1',
                isComplete: false,
        },
            {
                id: uuidv4(),
                title: 'viec2',
                isComplete: false,
        },
            {
                id: uuidv4(),
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

        const addTodo = newTodo =>{
            todos.value.push(newTodo)
        }

        return {
            todos,
            markCompleted,
            deleteItem,
            addTodo
            
        }    
    }
}
</script>

<style>

</style>