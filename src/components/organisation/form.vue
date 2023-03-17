<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >


      <q-input ref="typeRef" v-model="formData.organisation_name" type="char" mask="S" reverse-filled-mask label="Organisation Name*" :rules="[val => !!val || 'Field is required']"/>
      <q-input ref="typeRef" v-model="formData.prefix" label="Prefix*" :rules="[val => !!val || 'Field is required']"/>
      <q-input ref="typeRef" v-model="formData.description" type="char" label="Description"  />
      <q-input  v-model="formData.address" type="char" mask="S"  reverse-fill-mask label="Address"  />
      <q-input  v-model="formData.city" type="char" mask="S" reverse-fill-mask label="City" />

      <q-input ref="typeRef" v-model="formData.state" type="char" mask="S" reverse-fill-mask label="State" />
      <q-input v-model="formData.pin_code"  mask="#" reverse-fill-mask :rules="[ val => val.length == 6 || 'Please enter a valid pin code']" label="Pin Code"   />
      <q-input ref="typeRef" v-model="formData.contact_number" type="tel" mask="#" reverse-fill-mask :rules="[ val => val.length == 10 || 'Please enter a valid contact number']"  label="Contact" />
      <q-input v-model="formData.email" label="Email"  :rules="[ val => val.includes('@' && '.')||'Enter a valid email-id' ]"/>
      <q-input v-model="formData.gst_number"  mask="N" reverse-fill-mask label="GST number"  />
      <q-input  v-model="formData.pan_no"  mask="N" reverse-fill-mask label="PAN no" />
      <q-input  v-model="formData.invoices" label="Invoices" />
      <q-select ref="typeRef" clearable v-model="formData.status" label="status" :options="['Public','Draft','Archieved']" :rules="[val => !!val || 'Field is required']" />

      <q-input  v-model="formData.banks" label="banks"  />
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
      formData: {}
    }
  },
  methods: {
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
