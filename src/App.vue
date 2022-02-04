<template>
  <v-app>
    <v-main>
      <v-row justify="center" align="center">
      <v-col class="columna" cols="6">
        <v-row justify="center" aling="center">
          <h1>Listado de usuarios</h1>
        </v-row>
        <v-row justify="center">
          <v-data-table 
            :headers="headers"
            :items="listadoUsuarios"
            class = "elevation-2"
            hide-default-footer
            @click:row="gotoUser">
          </v-data-table>
        </v-row>
      </v-col>
      <v-col cols="6" class="columna">
        <v-row justify="center" aling="center">
          <user :user="itemUsuario"/>
        </v-row>
        <v-row justify="center" aling="center">
          <h1>Posts</h1>
        </v-row>
        <v-row justify="center" aling="center">
          <div class="scroll">
            <v-card id="posts" color="#70e7e7" v-for="(item, index) in postsUsuario" :key="index">
              <v-card-title>
                  {{item.title}}
              </v-card-title>
              <v-card-text> 
                {{item.body}}
              </v-card-text>
            </v-card>
          </div>
        </v-row>
      </v-col>
    </v-row>
    </v-main>
  </v-app>
</template>

<script>

import user from './components/usuario.vue'

export default {
  name: 'App',
  components: {
    user
  },

   data: () => {
    return {
      listadoUsuarios : [],
      postsUsuario: null,
      itemUsuario: null,
      headers: [
        {
          text: 'Usuario',
          align: 'center',
          sort: 'true',
          value: 'username'
        },
        {
          text: 'Correo electronico',
          aling: 'center',
          sort: 'false',
          value: 'email'
        }
      ]
    }
  },

  methods: {
    async obtenerListado(){
      try {
        const res = await fetch('https://jsonplaceholder.typicode.com/users')
        const data = await res.json()
        this.listadoUsuarios = data
        //console.log(this.listadoUsuarios)
      }
      catch (e) {
        console.log(e)
      }
    },
//////Ir al usuario
    gotoUser(user){
      //console.log(user)
      this.obtenerUser(user.id)
      this.obtenerPosts(user.id)
    },
//////Obtener posts
    async obtenerPosts (id) {
      try{
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/?userId=${id}`)
        const data = await res.json()
        this.postsUsuario = data
        console.log(data)

      }
      catch (e){
        console.log(e)
      }
    },
//////Obtener usuario
    async obtenerUser(id) {
      try{
        const res = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
        const data = await res.json()
        this.itemUsuario = data
        //console.log(data)

      }
      catch (e){
        console.log(e)
      }
    },
//////Random user
    randomUser() {
      const num = Math.round(Math.random()*10)
      const data = {
        id: num
      }
      this.gotoUser(data)
    }
  },

  created(){
    this.obtenerListado()
    this.randomUser()
  },
}
</script>

<style>
#posts {
  margin-top: 10px;
  border-radius: 10px;
  box-shadow: 10px 10;
  
}
.scroll {
  width: 500px;
  overflow: auto;
  height: 400px;
}
.columna{
  margin-top: 4%;
}

</style>