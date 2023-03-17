<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-input v-model="formData.sort" label="Sort" />
      <q-input v-model="formData.bank_name" type="char"  label="Bank name*" mask="S" reverse-fill-mask :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.account_name" type="char" label="Account Name*" mask="S" reverse-fill-mask :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.account_no" label="Account no*" mask="#" reverse-fill-mask :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.ifsc" label="IFSC*"  mask="N" reverse-fill-mask :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.branch" type="char" label="Branch" mask="S" reverse-fill-mask />
      <q-select clearable v-model="formData.organisation_id"  label="Organisation ID"
      :options="organisation" option-label="id" option-value="organisation_name" map-options emit-value />
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
      organisation:[]
    }
  },
  created () {
    this.fetchOrganisation()
  },
  methods: {
    async fetchOrganisation() {
      let response = await this.$api.get('items/organisation')
      this.organisation = response.data.data
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
