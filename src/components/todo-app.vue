<template>
    <ul>
        <li v-for="todo in todos"
            v-bind:key="todo.id">
            <input type="checkbox"
                @change="todo.completed = !todo.completed"
                >
            <span :class="{done: todo.completed}">{{todo.title}}</span>
            <button @click = "$emit('remove-item', todo.id)">Удалить</button>
        </li>
    </ul>
</template>

<script>
export default {
    // переменную с данными которую мы передали через в байнд помещаем в пропс
    props: ['todos'],
}
</script>


<style scoped>
    ul {
        
        padding: 0;

    }
    li {
        display: flex;
        list-style: none;
        margin: 0 20%;
        justify-content: space-between;
        align-items: center;
        border: 1px solid black;
        padding: 5px;
        margin-bottom: 10px;
        border-radius: 5px;
    }
    button {
        font-family: inherit;
        background-color: teal;
        color: white;
        border-radius: 5px;
        border: none;
    }
    .done {
        text-decoration: line-through;
    }
</style>