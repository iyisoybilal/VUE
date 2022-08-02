<template>
    <div id="addForm">
        <form @submit.prevent="handleAdd">
            <div class="form-group">
                <label for="id">Id</label>
                <input v-model="user.id" type="text" class="form-control" id="id">
            </div>
            <div class="form-group">
                <label for="userName">Ad</label>
                <input v-model="user.userName" type="text" class="form-control" id="userName">
            </div>
            <div class="form-group">
                <label for="userSurname">Soyad</label>
                <input v-model="user.userSurname" type="text" class="form-control" id="userSurname">
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <input v-model="user.email" type="text" class="form-control" id="email">
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input v-model="user.password" type="text" class="form-control" id="password">
            </div>
            <button type="submit" class="btn btn-sm btn-success">Ekle</button>
        </form>
    </div>
</template>
<script> 
export default {
    name:"user-add",
    data(){
        return {
        user: {
            id:"",
            userName:"",
            userSurname:"",
            email:"",
            password:""
             }
        };
    }, 
    methods:{
        handleAdd(){
            this.$emit("add:user",this.user) 
        }
    }
};
</script>
<style scoped>
#addForm{
   margin:100px;
}
</style>