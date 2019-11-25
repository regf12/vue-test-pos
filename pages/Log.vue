<template>
  <div class="container top">
    <div class="row justify-content-center">
      <div class="card">
        <div class="card-header">Consulta</div>
        <div class="card-body">
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
                    v-if="key!='id'&&key!='active'&&key!='created_at'&&key!='updated_at'">{{value}}</td>
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
        checks: [],
        aux: 0,
        data: [],
        fields: [
          'Ususario',
          'Acccion',
          'Tabla',
          'Elemento'
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
        this.$axios.get(`/log`)
          .then(response => {
            this.data = response.data.data;
          })
          .catch((e) => {
            console.error('error: ', e);
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
