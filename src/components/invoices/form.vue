<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-select   clearable v-model="formData.account_id" mask="S" reverse-fill-mask label="Account ID"
      :options="accounts" option-label="account_name" type="char" option-value="id" map-options emit-value />
      <q-input   v-model="formData.invoice_number" mask="#" reverse-fill-mask label="Invoice number" />
      <q-input ref="inputRef" clearable v-model="formData.invoice_date "  stack-label label="Invoice date *" :rules="[val => !!val || 'Field is required']" >
        <template v-slot:prepend>
        <q-icon name="schedule" class="cursor-pointer">
          <q-popup-proxy cover transition-show="scale" transition-hide="scale">
            <q-time v-model="formData.invoice_date" mask="YYYY-MM-DD HH:mm">
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-time>
          </q-popup-proxy>
        </q-icon>
      </template>
      <template v-slot:append>
        <q-icon name="event" class="cursor-pointer">
          <q-popup-proxy cover transition-show="scale" transition-hide="scale">
            <q-date v-model="formData.invoice_date" mask="YYYY-MM-DD HH:mm">
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-date>
          </q-popup-proxy>
        </q-icon>
      </template>
      </q-input>
      <q-input ref="inputRef" v-model="formData.grand_total" label="Grand total" />
      <q-select ref="inputRef" clearable v-model="formData.invoice_status" label="Invoice status" :options="['Draft','Provisional','Final','Cancelled']" :rules="[val => !!val || 'Field is required']"/>
      <q-select ref="inputRef" clearable v-model="formData.payment_status" label="Payment Status" :options="['Unpaid','Partially Paid','Paid']" :rules="[val => !!val || 'Field is required']"/>

      <q-select  clearable v-model="formData.organisation_id" label="Organisation ID"
      :options="organisation" option-label="id" type="char" option-value="organisation_name" map-options emit-value />
      <q-input  v-model="formData.invoice_details" type="char" label="Invoice Details" />
      <q-input  v-model="formData.invoice_settlement" label="Invoice settlment" />
      <q-input  v-model="formData.period" label="Period" />
      <q-select  v-model="formData.bank_id" label="Bank ID"
      :options="banks" option-label="id" mask="S" type="char" reverse-fill-mask option-value="bank_name"  />
      <q-input  v-model="formData.booked_by" label="Booked by" />
      <q-input v-model="formData.oncall_plan" label="Oncall plan" />
      <q-input  v-model="formData.vehicle_number" mask="#" reverse-fill-mask label="Vehicle number" />
      <q-input  v-model="formData.log_type" label="Log type"  />
      <q-input  v-model="formData.journey_date" stack-label label="Journey date" >
        <template v-slot:prepend>
        <q-icon name="schedule" class="cursor-pointer">
          <q-popup-proxy cover transition-show="scale" transition-hide="scale">
            <q-time v-model="formData.journey_date" mask="YYYY-MM-DD HH:mm">
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-time>
          </q-popup-proxy>
        </q-icon>
      </template>
<template v-slot:append>
        <q-icon name="event" class="cursor-pointer">
          <q-popup-proxy cover transition-show="scale" transition-hide="scale">
            <q-date v-model="formData.journey_date" mask="YYYY-MM-DD HH:mm">
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-date>
          </q-popup-proxy>
        </q-icon>
      </template>
</q-input>


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
      accounts: [],
      organisation: [],
      banks: []
    }
  },
  created () {
    this.fetchAccounts()
    this.fetchOrganisation()
    this.fetchBanks()
  },
  methods: {
    async fetchAccounts() {
      let response = await this.$api.get('items/accounts')
      this.accounts =response.data.data
    },
    async fetchOrganisation() {
      let response = await this.$api.get('items/organisation')
      this.organisation =response.data.data
    },
    async fetchBanks() {
      let response = await this.$api.get('items/banks')
      this.banks =response.data.data
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
