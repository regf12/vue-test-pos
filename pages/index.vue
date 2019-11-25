<template>
  <div class="container">
    <p v-if="loggedIn">
      <nav class="nav nav-pills flex-column flex-sm-row">
        <nuxt-link v-for="(ruta,key) in rutas" :key='key' class="flex-sm-fill text-sm-center nav-link"
          :class="($route.path==ruta.ruta)?'active':''" :to="ruta.ruta">{{ruta.name}}
        </nuxt-link>
      </nav>
    </p>
  </div>
</template>

<script>
  export default {
    mounted() {
      if (this.loggedIn) {
        this.$router.push('/consulta');
      }else{
        this.$router.push('/login');
      }
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

    methods: {}
  }

</script>
