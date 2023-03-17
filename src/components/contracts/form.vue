<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >


      <q-input v-model="formData.name" mask="S" reverse-fill-mask label="Name"  />
      <q-select clearable v-model="formData.account"
      :options="accounts" option-label= "id" type="char" option-value ="account_name" map-options emit-value label="Account"  />
      <q-input v-model="formData.vehicle_type" type="char" label="vehicle Type"  />
      <q-input v-model="formData.rent_per_month" mask="#" reverse-fill-mask  label="Rent per month"   />
      <q-select ref="inputRef" v-model="formData.fuel" label="Fuel*" :options ="['Including','Excluding']" :rules="[val => !!val || 'Field is required']"/>

      <q-input v-model="formData.log_book" label="Log Book"  />
      <q-toggle v-model="formData.is_tax_includes" label="Is tax included" :false-value="true"
      :label="`Model is ${redModel} (flipped boolean)`"
      :true-value="false"
      color="primary"
      type="redModel"
       keep-color
        />
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
