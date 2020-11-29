<template>
    <select v-model = "selectValue" @change= "$emit('check-value', selectValue)">
        <option value="all">Все</option>
        <option value="completed">Выполненные</option>
        <option value="not-completed">Не выполненные</option>
    </select>
</template>

<script>
export default {
    data() {
        return {
            selectValue: 'all'
        } 
    },
    // watch: {
    //     selectValue  (value) {
    //         console.log(value)
    //     }
    // },
    // methods: {
    //     value () {
    //         console.log(this.selectValue)
    //     }
    // }
}
</script>