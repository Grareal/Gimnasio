<template>
  <div class="fondo">
    <v-container fluid  >
    <v-layout align-center justify-center>
      <v-flex xs12 sm8 md4>
        <br>    <h1 v-bind:style="{ color: 'white' }">Sistema de administracion</h1>
<br><br><br>
        <v-card class="elevation-12" height="100%">
          <v-toolbar dark depressed:color="customColor">
            <v-toolbar-title>Iniciar sesión</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <v-form>
              <v-text-field
                prepend-icon="person"
                name="login"
                label="Usuario"
                type="text"
                v-model="usuario"
              ></v-text-field>
              <v-text-field
                id="password"
                prepend-icon="lock"
                name="password"
                label="Contraseña"
                type="password"
                v-model="password"
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="success" @click="iniciarSesion">Ingresar</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>

    </v-layout>
    <v-snackbar
        v-model="mostrarMensaje"
        :timeout="3000"
        :color="mensaje.color"
        top
        >
        {{ mensaje.texto }}
    </v-snackbar>
    </v-container>
 
  </div>
</template>
<script>
import HttpService from '../../Servicios/HttpService'

export default {
  name: "Login",

  data: () => ({
    customColor:"#F96A4C",
    usuario: "",
    password: "",
    mensaje: {
      texto: "",
      color: "",
    },
    mostrarMensaje: false
  }),

  methods: {
    iniciarSesion() {
      if (!this.usuario) {
          this.mostrarMensaje = true
          this.mensaje.texto = "Debes colocar el usuario"
          this.mensaje.color = "warning"
          return
      }
      if (!this.password) {
          this.mostrarMensaje = true
          this.mensaje.texto = "Debes colocar la contraseña"
          this.mensaje.color = "warning"
          return
      }
      let payload = {
          metodo: "login",
          usuario: {
              usuario:this.usuario,
              password: this.password
          }
      }
      HttpService.obtenerConDatos(payload, "usuarios.php")
      .then(resultado => {
          if(resultado) {
              this.$emit("logeado", resultado)
          }
      })

      
    },
  },
};
</script>
<style >
.fondo{
  border-top: 20px solid transparent;
  border-bottom: 20px solid transparent;
  border-right: 20px solid #FFA500;
  background-color: #3C3C3C;
  
}
</style>
