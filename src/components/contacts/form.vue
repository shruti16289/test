<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >


      <q-select clearable  v-model="formData.account_id" :options="accounts"
      option-label= "id" option-value ="account_name" map-options emit-value label="Account Id*" :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.designation" mask="S" reverse-fill-mask label="Designation" />
      <q-input v-model="formData.name" type="char" label="Name" mask="S" reverse-fill-mask :rules="[val => !!val || 'Field is required']" />
      <q-select clearable v-model="formData.status" label="Status" :options="['Published','Draft','Archieved']"/>
      <q-input v-model="formData.sort" label="Sort" />


  </q-form>
    </div>
    <div class="q-py-md">
      <q-btn color="red" label="submit" @click="submitData"></q-btn>
    </div>
    <div class="q-py-md">
      <q-btn color="red" label="close" to="./"></q-btn>
    </div>
  </q-card>

</template>
<script>

export default {
  data () {
    return {
      formData: {},
      accounts: []
    }
  },
  created () {
    this.fetchAccounts()
  },
  methods: {
    async fetchAccounts() {
    let response = await this.$api.get('items/accounts')
    this.accounts = response.data.data

    },
    async submitData () {
      let validation = await this.$refs.form.validate(true)
      if(validation){
        alert('Submitting Data to Backend')
      }
      else{
        alert('Form Validation Failed')
      }
  }
}
}
</script>
