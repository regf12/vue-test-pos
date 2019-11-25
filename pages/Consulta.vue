<template>
  <div class="container top">
    <div class="row justify-content-center">
        <div class="card">
          <div class="card-header">Consulta</div>
          <div class="card-body">

            <div class="row">
              <div class="col-sm-6">
                <input type="text" v-model="representante.name" class="form-control" id="inputPassword"
                  placeholder="Buscar por representante">
              </div>
              <button @click="fetch_shop();" class="btn btn-primary">
                Buscar
              </button>
            </div>

            <div class="clear-fix" ></div>

            <div class="table-responsive">
              <table class="table">

                <thead>
                  <tr>
                    <th scope="col">#</th>
                    <th v-for="(field,key) in fields" :key="key" scope="col">{{field}}</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(shop,index) in data" :key="index">
                    <th scope="row">
                      <input type="checkbox" class="form-check-input" id="" :value="shop.id" v-model="checks">
                      {{index}}
                    </th>
                    <td v-for="(value,key) in shop" :key="key"
                      v-if="key!='id'&&key!='active'&&key!='created_at'&&key!='updated_at'">{{value}}
                    </td>
                    <td>
                      <button @click="delete_shop(shop.id);" class="btn btn-danger">
                        Eliminar
                      </button>
                    </td>
                  </tr>
                </tbody>

              </table>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
  export default {
    layout: 'basic',
    data() {
      return {
        representante: {
          name: ''
        },
        checks:[],
        aux:0,
        data: [],
        fields: [
          'Comercio',
          'Representante',
          'Correo',
          'Telefono',
          'Pais',
          'Estado',
          'Ciudad',
          'Direccion',
          'Social',
          'Accion'
        ],
        userForm: {
          email: 'admin@mail.com',
          password: 'admin'
        }
      }
    },
    mounted() {
      if (!this.loggedIn) {
        this.$router.push('/login');
      }

      this.fetch_shop();
    },
    methods: {
      async loginUser() {
        await this.$auth.login({
          data: this.userForm
        });
        this.$router.push({
          path: '/'
        });
      },
      fetch_shop() {
        this.$axios.get(`/shop_get_filter`, this.representante.name)
          .then(response => {
            this.data = response.data.data;
          })
          .catch((e) => {
            alert('error: ', e);
          });
      },
      delete_shop(id) {
        this.$axios.delete(`/shop_destroy/${id}`)
          .then(response => {
            this.fetch_shop();
          })
          .catch((e) => {
            alert('error: ', e);
          });
      }
    }
  }

</script>

<style>
  .top {
    margin-top: 80px;
  }

</style>
