<template>
  <div class="container top">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="card">
          <div class="card-header">Comercios</div>
          <div class="card-body">
            <form @submit.prevent="registerComercio">

              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Nombre del Comercio</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.comercio" class="form-control" required autofocus>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Nombre del representante</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.cliente" class="form-control" required>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Correo electrónico</label>
                <div class="col-md-6">
                  <input type="email" v-model="Form.correo" class="form-control" required>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Teléfono</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.telefono" class="form-control" required>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Pais</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.pais" class="form-control" required>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Estado</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.estado" class="form-control" required>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Ciudad</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.ciudad" class="form-control" required>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">*Dirección</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.direccion" class="form-control" required>
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>
              <div class="form-group row">
                <label for="" class="col-sm-4 col-form-label text-md-right">Link a redes sociales</label>
                <div class="col-md-6">
                  <input type="text" v-model="Form.social" class="form-control">
                  <span class="invalid-feedback" role="alert">
                    <strong></strong>
                  </span>
                </div>
              </div>

              <div class="form-group row mb-0">
                <div class="col-md-8 offset-md-4">
                  <button type="submit" class="btn btn-primary">
                    Registrar
                  </button>
                </div>
              </div>

            </form>
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
        Form: {
          comercio: '',
          cliente: '',
          correo: '',
          telefono: '',
          pais: '',
          estado: '',
          ciudad: '',
          direccion: '',
          social: ''
        }
      }
    },
    mounted() {
      if (!this.loggedIn) {
        this.$router.push('/login');
      }
    },
    methods: {
      async registerComercio() {
        this.$axios.post(`/shop_store`, this.Form)
          .then(response => {
            this.$router.push('/consulta');
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
