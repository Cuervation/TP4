<template >

  <section class="src-componentes-formulario">
        <div class="jumbotron">
      <h2>Formulario</h2>
      <hr>
      <hr>
      <br>

      <vue-form :state="formState" @submit.prevent="guardar()">

        <!-- NOMBRE -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text" 
            id="nombre" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.nombre" 
            name="nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          >
          <!-- mensajes de validación -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="maxlength" class="alert alert-danger mt-1">
              Este campo debe poseer hasta {{ nombreMaxLength }} caracteres.
            </div>            


          </field-messages>
        </validate>
    
        <br>

        <!-- EDAD -->
        <validate tag="div">
          <label for="edad">Edad</label>
          <input 
            type="number" 
            id="edad" 
            class="form-control" 
            autocomplete="off"
            v-model.number="formData.edad" 
            name="edad"
            required
            :min="edadMin"
            :max="edadMax"
          >
          <!-- mensajes de validación -->
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">
              La edad mínima debe ser {{ edadMin }} años.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La edad máxima debe ser {{ edadMax }} años.
            </div>
          </field-messages>
        </validate>

        <br>

        <!-- MAIL -->
        <validate tag="div">
          <label for="email">Email</label>
          <input 
            type="email" 
            id="email" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.email" 
            name="email"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="email" class="alert alert-danger mt-1">Email no válido</div>
          </field-messages>
        </validate>
        <br>
        
      <button class="btn btn-danger my-3" :disabled="formState.$invalid">Guardar</button>
      </vue-form>    

      <hr>
      
      <div v-if="usuarios.length" class="table-responsive">
          <table class="table table-dark">
              <tr>
                  <th>#</th>                             
                  <th>Nombre</th>                  
                  <th>Edad</th>
                  <th>Email</th>                  
              </tr>
              <tr v-for="(usuario,index) in usuarios" :key="index">
                  <td>{{ index + 1 }}</td>
                  <td>{{ usuario.nombre }}</td>
                  <td>{{ usuario.edad }}</td>
                  <td>{{ usuario.email }}</td>
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
export default {
  name: "src-componentes-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      usuarios: [],
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 5,
      nombreMaxLength: 15,
      edadMin: 18,
      edadMax: 120,
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        edad: null,
        email: null,
      };
    },
    guardar() {
      this.usuarios.push({ ...this.formData });
      this.formData = this.getInitialData();
      this.formState._reset();
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.src-componentes-formulario {
}
  .jumbotron {
    background-color: rgb(8, 81, 94);
    color: white;
  }

  hr {
    background-color: #bbb;
  }
</style>
