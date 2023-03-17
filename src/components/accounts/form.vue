<template>
   <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md"  >

      <q-input ref="inputRef" v-model="formData.account_name"  type="char" mask="S" reverse-fill-mask label="Account Name *" :rules="[val => !!val || 'Field is required']" />
      <q-input ref="inputRef" v-model="formData.account_address" type="char" mask="S" reverse-fill-mask label="Account Address*" :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.contact_number" type="tel" mask="#" reverse-fill-mask label="Contact Number" />
      <q-input v-model="formData.e_mail" type="email"  :rules="[ val => val.includes('@' && '.')||'Enter a valid email-id' ]" label="Email" />
      <q-input v-model="formData.city"  type="char" mask="S" reverse-fill-mask label="City" />
      <q-input v-model="formData.state" type="char" label="State"  mask="S" reverse-fill-mask  />
      <q-input v-model="formData.pin_code"  mask="#" reverse-fill-mask :rules="[ val => val.length == 6 || 'Please enter a valid pin code']" label="Pin Code"   />
      <q-input v-model="formData.country" mask="S" reverse-fill-mask label="Country"  />
      <q-select clearable v-model="formData.accounting_receipts"
      :options="accounting_receipts" option-label="receipt_number" option-value="receipt_number" map-options emit-value label="Accounting Receipts"  />
      <q-select clearable v-model="formData.status" label="Status" :options="['Published','Draft','Archieved']"/>
      <q-select clearable v-model="formData.invoices"
      :options="invoices" option-label="invoice_number" option-value="invoice_number" map-options emit-value label="Invoices"   />
      <q-input v-model="formData.contacts" type="char" label="Contacts"   />
      <q-input v-model="formData.log_book" type="char" label="Log Book"  />
      <q-input v-model="formData.contracts" type="char" label="Contracts"  />
      <q-input v-model="formData.gst" label="GST"  />

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
  watch:{
    'formData.e_mail':{
      handler(val){
        this.formData.e_mail = val.toLowerCase()
      }
    }
  },
  data () {
    return {
      formData: {
        e_mail:''
      },
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
