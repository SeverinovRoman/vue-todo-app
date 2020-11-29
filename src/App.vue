// app.vue является основным родительским элементом, куда помещено все приложение
// тимплейт - шаблон куда помещается содержимое страницы
// Передаем данные в наш дочерний элемент - здесь как бы создаем переменнную которая будет хранить значение переданной тудус которая находится м дата 

<template>
  <div id="app">
    <h1>Vue ToDo Application</h1>
    <hr>
    <selectItem 
      @check-value = "checkValue"
    />
    <todoApp
      v-if = "filterTodos.length"
      v-bind:todos="filterTodos"
      @remove-item = "removeTodo"
    />
    <p v-else>Ничего нет!!!</p>
    <form @submit.prevent = "onSubmit">
      <input type="text" 
        v-model = "todoTitle">
      <button type="submit">Добавить</button>
    </form>
  </div>
</template>

// Скрипт предназначен для описания функционала. Сюда импортируем какие либо дочерние элементы
<script>
// import navigationBar from '@/components/navbar.vue'
import todoApp from '@/components/todo-app.vue'
import selectItem from '@/components/selected.vue'
// В экспорт дефолт помещаем имя компоненты, имена дочерних компонентов, а также данные, методы, фильтры а также вычисляемые свойства
export default {
  name: 'App',
  components: {
    todoApp,
    selectItem
  },
  data () {
    return {
      // вид массива айди тайтл комплитед
      // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
      todos: [],
      todoTitle: "",
      filterValue: ""
    }
  },
  methods: {
    // Метод реализует создание новой переменной при сабмите и помещении ее в наш массив туду 
    onSubmit () {
      if (this.todoTitle.trim()) {
        const newToDo = {
          userId: Date.now(),
          id: Date.now(),
          title: this.todoTitle,
          completed: false
        }
      this.todos.push(newToDo)
      console.log(this.todos)
      this.todoTitle = ""
      }
    },
    removeTodo (id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    checkValue (value) {
      this.filterValue = value
    }
  },
  
  // ПОЛУЧЕНИЕ ДАННЫХ С СЕРВЕРА И ДОБАВЛЕНИЕ ИХ В МАССИВ TODOS
  mounted () {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(response => response.json())
    // Позволяет взглянть на полученные данные
    //.then(json => console.log(json))
    .then(json => {
      this.todos = json
    })
  },
  computed: {
    filterTodos () {
      if (this.filterValue === 'completed') {
          return this.todos.filter(t => t.completed)
        }
      if (this.filterValue === 'not-completed') {
        return this.todos.filter(t => t.completed === false)
      }
      else {
        return this.todos
      }
    }
  }
}  
</script>


// Здесь пишем стили. если добавить атрибут SCOPED то стили будут применяться только для этого компонента.
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
form {
  display: flex;
  margin: 0 20%;
  justify-content: center;
  align-items: center;
}
form input {
  width: 75%;
  height: 20px;
  font-family: inherit;
  margin: 10px;
}
button {
  font-family: inherit;
  background-color: teal;
  color: white;
  border-radius: 5px;
  border: none;
}

</style>
