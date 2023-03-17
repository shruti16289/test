<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >



      <q-select clearable v-model="formData.account_id" :options="accounts" option-label= "id" option-value ="account_name" map-options emit-value label="Account ID" :rules="[ val => val && val.length > 0 || 'Please type something']" />
      <q-input  ref="inputRef" clearable v-model="formData.receipt_date"   stack-label label="Receipt Date   *" :rules="[val => !!val || 'Field is required']" >

        <template v-slot:prepend>
        <q-icon name="schedule" class="cursor-pointer">
          <q-popup-proxy cover transition-show="scale" transition-hide="scale">
            <q-time v-model="formData.receipt_date" mask="YYYY-MM-DD HH:mm">
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
            <q-date v-model="formData.receipt_date" mask="YYYY-MM-DD HH:mm">
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-date>
          </q-popup-proxy>
        </q-icon>

      </template>
</q-input>

      <q-input v-model="formData.receipt_number" mask="#"  reverse-filled-mask label="Receipt Number *" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.receipt_mode" label="Receipt Mode *"  :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.receipt_amount" mask="#"  reverse-fill-mask label="Receipt Amount" />
      <q-input v-model="formData.transaction_number" mask="#"  reverse-fill-mask label="Transaction number" />

      <q-select clearable v-model="formData.receipt_status" label="Receipt Status" :options="['Recieved','Cleared','Declined']" :rules="[ val => val && val.length > 0 || 'Please type something']" />
      <q-input v-model="formData.receipt_settlement" label="Receipt settlement" :rules="[ val => val && val.length > 0 || 'Please type something']" />

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
