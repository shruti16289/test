<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-select   clearable v-model="formData.account_id" label="Account ID" :options="accounts" option-label="id" option-value="id" map-options emit-value/>
      <q-select  clearable v-model="formData.vehicle_id" label="Vehicle ID" :options="vehicles" option-label="id" option-value="id" map-options emit-value />
      <q-select   clearable v-model="formData.contract_id" label="Contract ID" :options="contracts" option-label="id" option-value="id" map-options emit-value />
      <q-input   v-model="formData.date_from" label="Date from" />
      <q-select   clearable v-model="formData.contact_id" label="Contact ID" :options="contacts" option-label="id" option-value="id" map-options emit-value />
      <q-select  clearable v-model="formData.driver_id" label="Driver ID" :options="driver" option-label="id" option-value="id" map-options emit-value />
      <q-select ref="inputRef" v-model="formData.log_type" label="Log type" :options="['Monthly','Oncall']" :rules="[val => !!val || 'Field is required']" option-label="Standard"  />
      <q-input ref="inputRef" clearable v-model="formData.date_from" type="date" stack-label label="Date from *" :rules="[val => !!val || 'Field is required']"/>
      <q-input ref="inputRef" clearable v-model="formData.date_to"  type="date" stack-label label="Date to*" :rules="[val => !!val || 'Field is required']" />
      <q-input   v-model="formData.rent" label="Rent" />
      <q-input  v-model="formData.initial_reading" label="Initial reading"  />
      <q-input    v-model="formData.final_reading" label="Final reading" />
      <q-input   v-model="formData.running_kms" label="Running kms" />
      <q-input   v-model="formData.on_call_details" label="On call details" />
      <q-input   v-model="formData.extra_kms" label="Extra kms" />
      <q-input   v-model="formData.days" label="Days" />
      <q-input   v-model="formData.night_halt_charges" label="Night halt charges"/>
      <q-input   v-model="formData.amount" mask="#" reverse-fill-mask label="Amount" />
      <q-select   v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       option-label="Standard" :rules="[val => !!val || 'Field is required']"/>
      <q-toggle  ref="inputRef" v-model="formData.is_invoiced" label="Is invoiced" :false-value="true" :rules="[val => !!val || 'Field is required']"
      :label="`Model is ${redModel} (flipped boolean)`"
      :true-value="false"
      color="primary"
      type="redModel"
      keep-color
 />
      <q-toggle   ref="inputRef" v-model="formData.is_paid" label="Is paid" :false-value="true" :rules="[val => !!val || 'Field is required']"
      :label="`Model is ${redModel} (flipped boolean)`"
      :true-value="false"
      color="primary"
      type="redModel"
      keep-color
 />
      <q-input  ref="inputRef" v-model="formData.sort" label="Sort" :rules="[val => !!val || 'Field is required']"/>
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
      vehicles: [],
      contracts: [],
      contacts: [],
      driver: []
    }
  },
  created () {
    this.fetchAccounts()
    this.fetchVehicles()
    this.fetchContracts()
    this.fetchContacts()
    this.fetchDriver()
  },
  methods: {
    async fetchAccounts() {
      let response = await this.$api.get('items/accounts')
      this.accounts =response.data.data
    },
    async fetchVehicles() {
      let response = await this.$api.get('items/vehicles')
      this.vehicles =response.data.data
    },
    async fetchContracts() {
      let response = await this.$api.get('items/contracts')
      this.contracts =response.data.data
    },
    async fetchContacts() {
      let response = await this.$api.get('items/contacts')
      this.contacts =response.data.data
    },
    async fetchDriver() {
      let response = await this.$api.get('items/driver')
      this.driver =response.data.data
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
