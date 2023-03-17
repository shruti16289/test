<template>
  <q-page class="flex flex-center">
  <div>
  <q-card class="q-pa-md q-gutter-sm">
  <h5>Login to Proceed</h5>
  <q-input v-model="formData.email" label="Username" />
  <q-input v-model="formData.password" label="password" />
  <div class ="row q-my-md justify-center">
  <q-btn class="col" unelevated color="green" label="Login" @click="register"/>
  </div>
    formData - {{ formData }}
    <br>
    Response - {{  response }}

  </q-card>
  </div>
  </q-page>
</template>
<script>
export default {
  data() {
    return{
      formData: {
        mode: 'json'
      },
      response: null

    }
  },
  methods: {
    async login(){
      let response = await this.$api.post('https://gangotri-api.brainysoftwares.com/auth/login',this.formData)
      this.response = response.data
      this.$api.defaults.headers.common['authorization'] = ' Bearer ' + response.data.data.access_token

      this.$router.push('./modules/gangotri')
    }
  }
}
</script>
