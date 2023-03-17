<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-input  v-model="formData.sort" label="Sort" />
       <q-input ref="typeRef" v-model="formData.vehicle_type" type="char" mask="S" reverse-fill-mask label="Vehicle type*" :rules="[val => !!val || 'Field is required']"/>
      <q-input ref="typeRef" v-model="formData.vehicles" type="char" mask="S" reverse-fill-mask label="Vehicles*" :rules="[val => !!val || 'Field is required']"/>
      <q-input  v-model="formData.contracts" label="Contracts" />
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
