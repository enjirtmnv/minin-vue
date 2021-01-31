<template>
    <li>
        <span v-bind:class="{done: item.completed}">
            <input type="checkbox" v-on:change="item.completed = !item.completed">
            <strong>{{index + 1}}</strong>
                    {{item.title | uppercase}}
        </span>
        <button class="rm" v-on:click="$emit('remove-item', item.id)">&times;</button>
    </li>
</template>

<script>

    // filters - трансформируют данные внутри шаблона

    export default {
        props: {
            item: {
                type: Object,
                required: true
            },
            index: Number,
        },
        filters: {
            uppercase(value) {
                console.log(value);
                return value.toUpperCase()
            }
        }
    }
</script>

<style scoped>
    li {
        border: 1px solid hotpink;
        display: flex;
        justify-content: space-between;
        padding: 0.5rem 2rem;
        margin-bottom: 1rem;
        background-color: lightpink;
    }
    .rm{
        background-color: purple;
        color: aqua;
        border-radius: 50%;
        font-weight: bold;
    }
    input{
        margin-right: 1rem;
    }
    .done{
        text-decoration: line-through;
    }
</style>