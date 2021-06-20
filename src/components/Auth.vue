<template>
    <div>
        <div>
            <label>Username : </label>
            <input type="text" v-model="username"/>
        </div>
        <div>
            <label>Password : </label>
            <input type="password" v-model="password">
        </div>

        <button @click="saveBtn">Save</button>
        <button @click="deleteBtn"> Delete</button>
    </div>
</template>

<script>
export default {
    data : function() {
        return {
            username : '',
            password : ''
        }
    },
    created:function(){
        this.username = localStorage.getItem('user')
        this.password = localStorage.getItem('pass')
    },
    methods:{
        saveBtn : function (){
            localStorage.setItem('user',this.username)
            localStorage.setItem('pass',this.password)
        },
        deleteBtn : function (){
            localStorage.removeItem('user')
            localStorage.removeItem('pass')
            this.username = ''
            this.password = ''
        }
    }
}
</script>