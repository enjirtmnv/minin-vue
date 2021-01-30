<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button type="submit">Create</button>
    </form>
</template>

<script>
    export default {
        data() {
            return{
                title: '',
            }
        },
        methods: {
            onSubmit() {
                if (this.title.trim()){
                    const newItem = {
                        id: Date.now(),
                        title: this.title,
                        completed: false,
                    };

                    this.$emit('add-item', newItem);
                    this.title = ''
                }
            }
        }
    }
</script>

<style scoped>
    form{
        display: flex;
        justify-content: center;
        margin: 2rem 0;
    }

    input{
        width: 400px;
        height: 30px;
        background-color: #aefffd;
    }

    button{
        background-color: aqua;
        font-weight: bold;
    }

</style>