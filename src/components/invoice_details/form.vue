<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-input  v-model="formData.item_id" label="Item ID" />
      <q-input   v-model="formData.rate" label="Rate" />
      <q-input clearable  v-model="formData.receipt_date"  type="date" stack-label label="Receipt Date   *" />
      <q-input  ref="inputRef" v-model="formData.quantity" mask="#" reverse-fill-mask label="Quantity *" :rules="[val => !!val || 'Field is required']"  />
      <q-input ref="inputRef" v-model="formData.amount"  mask="#" reverse-fill-mask label="Amount*" :rules="[val => !!val || 'Field is required']" />
      <q-input  v-model="formData.tax_rate" label="Tax Rate" />
      <q-input v-model="formData.tax_amount" mask="#" reverse-fill-mask label="Tax amount" />
      <q-input  v-model="formData.total_amount" mask="#" reverse-fill-mask label="Total amount" />
      <q-select  clearable v-model="formData.status" label="Status" :options="['Published','Draft','Archieved']" :rules="[val => !!val || 'Field is required']"/>
      <q-select   clearable v-model="formData.invoice_id" label="Invoice ID" :options="invoices" option-label="id" option-value="id" map-options emit-value :rules="[val => !!val || 'Field is required']"/>
      <q-input  v-model="formData.description" type="char" mask="S" reverse-fill-mask  label="Description" />
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
      invoices: []
    }
  },
  created () {
    this.fetchInvoices()
  },
  methods: {
    async fetchInvoices() {
    let response = await this.$api.get('items/invoices')
    this.invoices = response.data.data

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
