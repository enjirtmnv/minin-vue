<template>
    <div>
        <h2>App items</h2>
        <AddItem
                @add-item="addItem"
        />
        <select v-model="filter">
            <option value="all">All</option>
            <option value="completed">Completed</option>
            <option value="not-completed">Not Completed</option>
        </select>
        <Loader v-if="loading === true"/>
        <TodoList
                v-else-if="filteredItems.length"
                v-bind:todos="filteredItems"
                @remove-item="removeItem"
        />
        <p v-else>No items!</p>
        <router-link to="/">Home</router-link>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddItem from '@/components/AddItem'
    import Loader from '@/components/Loader'

    export default {
        name: 'App',
        data() {
            return {
                todos: [
                    // {id: 1, title: 'gucci gang', completed: false},
                    // {id: 2, title: 'prada re-edition 2005', completed: false},
                    // {id: 3, title: 'off-white', completed: false},
                ],
                loading: true,
                filter: 'all'
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
                .then(response => response.json())
                .then(json => {
                        setTimeout(() => {
                            this.todos = json;
                            this.loading = false
                        }, 1000)
                    }
                )
        },
        // watch: {
        //     filter(value){
        //         console.log(value)
        //     }
        // },
        computed: {
            filteredItems() {
                if (this.filter === 'all' ){
                    return this.todos
                }

                if (this.filter === 'completed' ){
                    return this.todos.filter(t => t.completed)
                }

                if (this.filter === 'completed' ){
                    return this.todos.filter(t => !t.completed)
                }
            }
        },
        methods: {
            removeItem(id) {
                this.todos = this.todos.filter(i => id !== i.id)
            },
            addItem(newItem) {
                this.todos.push(newItem);
                console.log(this.todos)
            }
        },
        components: {
            TodoList, AddItem, Loader
        }
    }
</script>