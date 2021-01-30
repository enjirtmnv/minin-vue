<template>
    <div>
        <h2>App items</h2>
        <AddItem
                @add-item="addItem"
        />
        <TodoList
                v-if="todos.length"
                v-bind:todos="todos"
                @remove-item="removeItem"
        />
        <p v-else>No items!</p>
        <router-link to="/">Home</router-link>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddItem from '@/components/AddItem'
    export default {
        name: 'App',
        data() {
            return{
                todos: [
                    // {id: 1, title: 'gucci gang', completed: false},
                    // {id: 2, title: 'prada re-edition 2005', completed: false},
                    // {id: 3, title: 'off-white', completed: false},
                ]
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
                .then(response => response.json())
                .then(json =>
                    this.todos = json
                )
        },
        methods: {
            removeItem(id) {
                this.todos = this.todos.filter(i => id !== i.id)
            },
            addItem(newItem){
                this.todos.push(newItem);
                console.log(this.todos)
            }
        },
        components: {
            TodoList, AddItem
        }
    }
</script>