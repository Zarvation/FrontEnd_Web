<template>
  <div>
    <h1>Selamat Datang</h1>
    <div>Berikut daftar kerja kita : </div>
    <ul>
      <li v-for="item in todos" :key="item">{{item.name}}<button @click ="deleteTodos(item.name)">-</button></li> 
    </ul>
    <input v-model="myText" type="text"/>
    <button @click="addTodos">Add</button>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data: () => {
      return {
        todos: [],
        myText:''
      }
    },
    mounted: function(){
      this.getTodos()
    },
    methods: {
        getTodos() {
            const username = localStorage.getItem('usr')
            const password = localStorage.getItem('pwd')
            axios.get('http://localhost:3000/todo', { headers: { username, password }} )
            .then(result => {
              this.todos = result.data
            })
      },
        addTodos() {
            const username = localStorage.getItem('usr')
            const password = localStorage.getItem('pwd')
            let addItem = {name: this.myText}
                axios.post('http://localhost:3000/todo', addItem, { headers: { username, password } })
            this.todos.push(addItem)
      },
        deleteTodos(name) {
            const username = localStorage.getItem('usr')
            const password = localStorage.getItem('pwd')
            axios.delete(`http://localhost:3000/todo/${name}`, { headers: { username, password } })
            .then(() => {
                this.getTodos()
            })
      }
    }
  }
</script>

