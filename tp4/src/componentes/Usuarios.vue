<template >

  <section class="src-componentes-usuarios">
     <div class="jumbotron">
      <h2>Usuarios</h2>
      <hr />
      <hr />
      <br />

      <button class="btn btn-danger my-3 mr-3" @click="getUsuariosXHRPromise()">
        Pedir XMLHttpRequest
      </button>
      <button class="btn btn-info my-3 mr-3" @click="getUsuariosFetchAsync()">        
        Pedir Fetch
      </button>
      <button class="btn btn-danger my-3 mr-3" @click="getUsuariosAxios()">
        Pedir Axios
      </button>

      <button class="btn btn-info my-3 mr-3" @click="usuarios = []">
        Limpiar
      </button>
      <br />

      <div v-if="usuarios.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>id</th>
            <th>nombre</th>
            <th>email</th>
            <th>teléfono</th>
          </tr>          
          <tr v-for="usuario in usuarios" :key="usuario.id">
            <td>{{ usuario.id }}</td>
            <td>{{ usuario.nombre }}</td>
            <td>{{ usuario.email }}</td>
            <td>{{ usuario.telefono }}</td>
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-danger text-center">
        No se encuentran datos
      </h4>
    </div>
  </section>

</template>

<script >

  export default  {
    name: 'src-componentes-usuarios',
    props: [],
    mounted () {

    },
    data () {
      return {
        url : 'https://6340a92d16ffb7e275c3ec80.mockapi.io/usuarios2',
        usuarios : []
      }
    },
    methods: {
        xhrPromise() {
          return new Promise((resolve, reject) => {
            const xhr = new XMLHttpRequest();
            xhr.open("get", this.url);
            xhr.addEventListener("load", () => {
              if (xhr.status == 200) {
                let respuesta = JSON.parse(xhr.response);
                resolve(respuesta);
              } else {
                reject(`Error http : ,${xhr.status}`);
              }
            });
            xhr.send();
          });
        },
        getUsuariosXHRPromise() {          
          this.xhrPromise()
            .then((respuesta) => {
              this.usuarios = respuesta;
            })
            .catch((error) => console.log(error));
        },  
        async getUsuariosFetchAsync() {                
          try {
            let response = await fetch(this.url)        
            let respuesta = await response.json();       
            this.usuarios = respuesta;
          }
          catch(error) {
            console.log(error);
          }          

            
        },  

        getUsuariosAxios() {          
        this.axios(this.url)
          .then( respuesta => {this.usuarios = respuesta.data })
          .catch((error) => console.log(error))       
      },
      },   
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-usuarios {

  }

  .jumbotron {
    background-color: rgb(75, 87, 89);
    color: white;
  }

  hr {
    background-color: #bbb;
  }

</style>
