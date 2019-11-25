<template>
  <div>
    <Navbar />

    <nav class="nav nav-pills flex-column flex-sm-row">
      <nuxt-link v-for="(ruta,key) in rutas" :key='key' class="flex-sm-fill text-sm-center nav-link"
        :class="($route.path==ruta.ruta)?'active':''" :to="ruta.ruta">{{ruta.name}}
      </nuxt-link>
    </nav>

    <nuxt />
  </div>
</template>
<script>
  import Navbar from './partials/Navbar';
  export default {
    components: {
      Navbar
    },

    data() {
      return {
        rutas: [{
            ruta: '/consulta',
            name: 'Consulta'
          },
          {
            ruta: '/comercios',
            name: 'Comercios'
          },
          {
            ruta: '/log',
            name: 'Log'
          }
        ]
      }
    },

    computed: {

    },

    methods: {

    }


  }

</script>
