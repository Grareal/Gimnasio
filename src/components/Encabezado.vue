<template>
  <div>
       <v-app-bar depressed:color="'#'+colorsin.base" class="flex-grow-0 orange" app dark>

       <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>

        <!-- Esta parte es del logo superior-->
        <img src="@/assets/logo.png" width="100" height="70">
      </v-toolbar-title>
      <v-spacer></v-spacer>

      <v-btn icon @click="salir">
        <v-icon>logout</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer app v-model="drawer" class="fondo">
      <v-list-item>
        <!-- Esta parte es del logo pequeño con el nombre de la empresa-->
        <v-list-item-content>
          <v-list-item-title class="text-h6 black--text"> 
            <v-avatar>
              <img
                :src="urlImagen(logo)"
                alt="Logo"
              >
            </v-avatar>
            {{ nombreGimnasio }}
            </v-list-item-title>
          <v-list-item-subtitle class="text-h6 black--text"> {{ nombreUsuario }} </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <!--AQUI VA EL NAV BAR LATERAL!-->
      <v-divider></v-divider>
      <v-list dense nav>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          :to="item.link"
          class="black--text"
        >
          <v-list-item-icon >
            <v-icon class="black--text">{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>
<script>
import Utiles from '../Servicios/Utiles'
export default {
  name: "Encabezado",
 

  data: () => ({
    drawer: false,
    nombreUsuario: "",
    nombreGimnasio: "",
    logo: "",
   //ESTOS DE AQUI SON LOS ITEMS LATERALES CON SU TITULO, ICONO Y A DONDE REDIRIGE
    items: [
      { title: "Inicio", icon: "mdi-view-dashboard", link: "/" },
      { title: "Visitas", icon: "mdi-calendar-star", link: "/visitas" },
      { title: "Usuarios", icon: "mdi-account-box", link: "/usuarios" },
      { title: "Miembros", icon: "mdi-weight-lifter", link: "/miembros" },
      {
        title: "Membresías",
        icon: "mdi-wallet-membership",
        link: "/membresias",
      },
       { title: "Configurar", icon: "mdi-cog", link: "/configurar" },
      { title: "Mi perfil", icon: "mdi-account-key", link: "/perfil" },
    ],
  }),

  mounted(){
    this.nombreUsuario = localStorage.getItem("nombreUsuario")
    this.nombreGimnasio = localStorage.getItem("nombreGimnasio")
    this.logo = localStorage.getItem("logoGimnasio")

  },

  methods:{ 
    salir(){
      localStorage.removeItem('logeado')
      localStorage.removeItem('nombreUsuario')
      localStorage.removeItem('idUsuario')
      window.location.reload()
    },

    urlImagen(imagen) {
      return Utiles.generarURL(imagen);
    },

  }
};
</script>
<style>

</style>
