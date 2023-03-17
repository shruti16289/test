<template>

<q-card class="q-pa-md  scroll" style="height: 580px">
  {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >


      <q-input ref=inputRef v-model="formData.tax_name" mask="S" reverse-fill-mask label="Tax name" :rules="[ val => val && val.length > 0 || 'Please type something']" />
      <q-input ref=inputRef v-model="formData.tax_rate" mask="#" reverse-fill-mask label="Tax rate" :rules="[ val => val && val.length > 0 || 'Please type something']"/>
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
