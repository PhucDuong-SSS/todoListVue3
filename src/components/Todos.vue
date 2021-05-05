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
// import {v4 as uuidv4} from 'uuid';
import axios from 'axios';

export default {
    name: 'Todos',
    components : {TodoItem, AddTodo},
    setup()
    {
        const todos = ref([]);

        const getAllTodo = async () =>
        {
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
                todos.value = res.data  
            } catch (error) {
                console.log(error);
            }
        }
        const markCompleted = id => {
            todos.value = todos.value.map(todo =>{
                if(todo.id == id) todo.isComplete = !todo.isComplete;
                return todo
            });
}
        const deleteItem = async id =>{
            // todos.value = todos.value.filter(todo => todo.id !== id 
            // );
            try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
                todos.value = todos.value.filter(todo => todo.id !== id );
            } catch (error) {   
                console.log(error)
                
            }
        }

        const addTodo = async newTodo =>{
            try {
                const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newTodo);
                todos.value.push(res.data);
            } catch (error) {
                console.log(error);
            }
            // todos.value.push(newTodo)
        }

        getAllTodo()

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