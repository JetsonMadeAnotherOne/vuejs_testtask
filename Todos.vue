<template>
    <div>
        <h1>Todo application</h1>
        <AddTodo
                @add-todo="addTodo"
        />
        <TodoList
                v-bind:todos="todos"
                @remove-todo="removeTodo"
        />
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddTodo from '@/components/AddTodo'
    export default {
        name: 'app',
        data(){
            return{
                todos:[]
            }
        },
        mounted(){
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
                .then(response => response.json())
                .then(json => {
                    this.todos = json
                })
        },
        methods:{
            removeTodo(id){
                this.todos = this.todos.filter(t => t.id !== id)
            },
            addTodo(todo){
                this.todos.push(todo)
            }
        },
        components: {
            TodoList,AddTodo
        }
    }
</script>

<style scoped>

</style>