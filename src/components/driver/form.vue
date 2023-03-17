<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-input v-model="formData.driver_name" type="char"  mask="S" reverse-fill-mask label="Driver Name" :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.address" type="char" label="address" mask="S" reverse-fill-mask />
      <q-input v-model="formData.contact_no" type="tel" mask="#" reverse-fill-mask :rules="[ val => val.length == 10 || 'Please enter a valid contact number']"  label="Contact number" />
      <q-select clearable v-model="formData.status" label="Status" :options="['Published','Draft','Archieved']" :rules="[val => !!val || 'Field is required']"/>
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
