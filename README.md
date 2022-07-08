# vue-2_delete-record

run json-server --watch db.json

#1. Users.vue
<template>
  <div>
     
        <table border="1px">
            <tr>
              <td>Name</td>
              <td>Email</td>
              <td>Address</td>
              <td>Action</td>
            </tr>
            <tr v-for="user in users" v-bind:key="user.id">
              <td>{{user.name}}</td>
              <td>{{user.email}}</td>
              <td>{{user.address}}</td>
              <td><button v-on:click="deleteUser(user.id)">Delete</button></td>
              <td><button v-on:click="editUser(user.id)">Edit</button></td>
          </tr>
      </table>
  </div>
</template>

<script>
// import * as Vue from 'vue' // in Vue 3
import Vue from 'vue'   // in Vue 2
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios) //Bind axios 3 files
export default {
    name: "Delete-User",
    data(){
        return{
            users:null,
            user:{
                name:null,
                email:null,
                address:null
            }
        }
    },
    methods:{
       
        getUsers(){
            this.axios.get('http://localhost:3000/users').then((result) =>{
                console.log(result)
                this.users=result.data
            })
        },
      
        deleteUser(id){
            this.axios.delete('http://localhost:3000/users/'+id).then((result) =>{
                console.log(result)
                this.getUsers()
            })
        }
    },
    mounted(){
        this.getUsers()
    }
}
</script>

<style>

</style>
## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
