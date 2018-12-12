<template>
  <div class="container">
    <div class="col-lg-6 offset-lg-3">
      <div v-if="success" class="alert alert-success" role="alert">
        Assinatura realizada com sucesso!
      </div>
      <div v-if="errors" class="alert alert-danger" role="alert">
        <div v-for="(value, key) in errors">{{ value[0] }}</div>
      </div>
      <h2>{{ msg }}</h2>
      <form>
        <div class="form-group">
          <h3>Dados do Usuário</h3>
          <input type="text" class="form-control" v-model="order.user.name" placeholder="Nome" />
          <input type="text" class="form-control" v-model="order.user.email" placeholder="Email" />
          <input type="text" class="form-control" v-model="order.user.cpf" placeholder="CPF" />
        </div>
        <div class="form-group">
          <h3>Dados do Usuário</h3>
          <input type="text" class="form-control" v-model="order.user.orders_attributes[0].model" placeholder="Model" />
          <input type="text" class="form-control" v-model="order.user.orders_attributes[0].imei" placeholder="IMEI" />
          <input type="text" class="form-control" v-model="order.user.orders_attributes[0].price" placeholder="Preço" />
          <input type="text" class="form-control" v-model="order.user.orders_attributes[0].payment_installments" placeholder="Parcelas" />
        </div>
        <button @click.prevent="cadastrar" class="btn btn-success">Cadastrar</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Order',
  props: {
    msg: String
  },
  data: function () {
    return {
      order: {
        user: {
          name: '',
          email: '',
          cpf: '',
          orders_attributes: [
              {
                model: '',
                imei: '',
                price: '',
                payment_installments: ''
            }
          ]
        }
      },
      success: false,
      errors: null
    }
  },
  methods: {
    cadastrar: function() {
      axios.post(`http://localhost:3000/users`, this.order)
      .then(response => {
        this.success = true
      })
      .catch(error => {
        this.errors = error.response.data;
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-control {
  margin: 10px;
}
</style>
