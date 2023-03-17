<template>
  <q-card class="q-pa-md scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >


      <q-select clearable v-model="formData.invoice_id"
      :options="invoices" option-label= "id" option-value ="id" map-options emit-value label="Invoice ID"   />
      <q-select clearable v-model="formData.receipt_id"
      :options="accounting_receipts" option-label= "id" option-value ="id" map-options emit-value label="Receipt ID"  />
      <q-input  ref="inputRef" v-model="formData.amount" mask="#" reverse-fill-mask label="Amount*" :rules="[val => !!val || 'Field is required']"/>

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
      invoices: [],
      accounting_receipts: []
    }
  },
  created () {
    this.fetchInvoices()
    this.fetchAccounting()
  },
  methods: {

    async fetchInvoices() {
    let response = await this.$api.get('items/invoices')
    this.invoices = response.data.data
    },
    async fetchAccounting() {
    let response = await this.$api.get('items/accounting_receipts')
    this.accounting_receipts = response.data.data

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
