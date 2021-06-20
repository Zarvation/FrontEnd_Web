<template>
    <div>
        <ul>
            <li v-for="item in users" :key="item">{{item.username}} <button @click="deleteUser(item.id)">X</button></li>
        </ul>
        <input v-model="username" type="text" placeholder="Username">
        <br />
        <input v-model="password" type="password" placeholder="Password">
        <br />
        <button @click="addUser">Add</button>
    </div>
</template>

<script>import axios from 'axios'
  export default {
    data: () => {
      return {
        users: [],
        username: '',
        password: ''
      }
    },
    mounted: function(){
      this.getUser()
    },
    methods: {
        getUser() {
            const username = localStorage.getItem('usr')
            const password = localStorage.getItem('pwd')
            axios.get('http://localhost:3000/user/users', { headers: { username, password } })
            .then(result => {
                this.users = result.data
            })
      },
        addUser() {
            const username = localStorage.getItem('usr')
            const password = localStorage.getItem('pwd')
            let addUser = { username: this.username, password: this.password}
            axios.post('http://localhost:3000/user', addUser, { headers: { username, password } })
            this.users.push(addUser)
      },
        deleteUser(id) {
            const username = localStorage.getItem('usr')
            const password = localStorage.getItem('pwd')
            axios.delete(`http://localhost:3000/user/${id}`, { headers: { username, password } })
              .then(() => {
                this.getUser()
              })
      }
    }
  }</script>

