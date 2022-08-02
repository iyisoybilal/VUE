<template>
    <div id="list">
        <p v-if="users.length==0">Kullanıcı Listesi Boş</p>
        <table v-else class="table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>userName</th>
                    <th>userSurname</th>
                    <th>email</th>
                    <th>password</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user.id">
               <td v-if="updateId===user.id">
                    <input v-model="user.id" type="text" class="form-control" id="id" />
               </td> 
               <td v-else>
                    {{user.id}}
               </td>
               <td v-if="updateId===user.id">
                    <input v-model="user.userName" type="text" class="form-control" id="id" />
               </td> 
               <td v-else> 
                    {{user.userName}}
               </td>
               <td v-if="updateId===user.id">
                    <input v-model="user.userSurname" type="text" class="form-control" id="id" />
               </td> 
               <td v-else>
                    {{user.userSurname}}
               </td>
               <td v-if="updateId===user.id">
                    <input v-model="user.email" type="text" class="form-control" id="id" />
               </td> 
               <td v-else>
                    {{user.email}}
               </td>
               <td v-if="updateId===user.id">
                    <input v-model="user.password" type="text" class="form-control" id="id" />
               </td> 
               <td v-else>
                    {{user.password}}
               </td>
               <td v-if="updateId !==user.id">
                <button class="btn btn-sm btn-primary" @click="handleUpdate(user)">Güncelle</button>
                <button class="btn btn-sm btn-danger" @click="handleDelete(user)">Sil</button>
               </td>
                <td v-else>
                 <button class="btn btn-sm btn-primary" @click="handleSave(user)">Kaydet</button>
                 <button class="btn btn-sm btn-danger" @click="updateId=null">İptal</button>
                </td>
                </tr>
            </tbody>

        </table>
    </div>
</template>
<script>
export default {
    name:"user-list",
    data(){
        return{
            updateId:null
        };
    },
    props:{
        users:Array
    },
    methods:{
        handleDelete(user){
            this.$emit("delete:user",user)
        },
        handleUpdate(user){
            this.updateId=user.id
        },
        handleSave(user){
            this.$emit("update:user",user)
            this.updateId=null
        }
    }
};
</script>

<style scoped>
#list{
   margin:100px;
}
</style>