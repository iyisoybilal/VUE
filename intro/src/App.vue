<template>
  <div id="app">
    <userAdd @add:user="addUser"/>
     <userList @delete:user="deleteUser" @update:user="updateUser" :users="users"/>
  </div>
</template>

<script>
import userList from './components/userList.vue'
import userAdd from './components/userAdd.vue'

export default {
  name: 'app',
  components: {
    userList,
    userAdd
  },
  data(){
    return{
      users:[]
    }
  },
  mounted(){
    this.getUsers()
  },
  methods:{
    async getUsers(){
      const result = await fetch('http://localhost:3000/users')
      const data = await result.json()
      this.users=data;
    },
    async deleteUser(user){
      await fetch('http://localhost:3000/users/'+user.id,{
        method:'DELETE'
      })
      this.users=this.users.filter(
        userToFilter=>userToFilter.id!==user.id
      )
    },
    async updateUser(user){
        const result = await fetch('http://localhost:3000/users/'+user.id,{
        method:'PUT',
        body:JSON.stringify(user),
        headers:{"Content-Type":"application/json"}
      })
      const updatedUser = await result.json()
      this.users = this.users.map(user=>user.id===updatedUser.id?updatedUser:user)

    },
    async addUser(user){
        const result = await fetch('http://localhost:3000/users',{
        method:'POST',
        body:JSON.stringify(user),
        headers:{"Content-Type":"application/json"}
      })
      const newUser = await result.json()
      this.users = [...this.users,newUser]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
