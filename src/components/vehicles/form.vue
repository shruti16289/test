<template>
  <q-card class="q-pa-md  scroll" style="height: 580px">
    <q-pull-to-refresh @refresh="refresh">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >
      
      <q-input ref="typeRef" v-model="formData.vehicle_no"  mask="N" reverse-fill-mask label="Vehicle No.*" :rules="[val => !!val || 'Field is required']" />
      <q-select ref="typeRef" clearable v-model="formData.vehicle_type"
      :options="vehicle_type" option-label="vehicle_type" option-value="vehicle_type" map-options emit-value label="Vehicle type*" :rules="[val => !!val || 'Field is required']"/>
      <q-select ref="typeRef" v-model="formData.status" label="Status*" :options="['Published','Draft','Archieved']" :rules="[val => !!val || 'Field is required']"/>
      <q-input ref="typeRef" v-model="formData.sort"  mask="S" reverse-fill-mask label="Sort*" :rules="[val => !!val || 'Field is required']" />
      <q-input  v-model="formData.fuel_avg" label="Fuel" />
      <q-input  v-model="formData.log_book" label="Log book" />

</q-form>
    </div>
    <div class="q-py-md">
      <q-btn color="red" label="submit" @click="submitData"></q-btn>
    </div>
    <div class="q-py-md">
      <q-btn color="red" label="close" to="./"></q-btn>

    </div>
  </q-pull-to-refresh>
  </q-card>

</template>
<script>
export default {
  data () {
    return {
      formData: {},
      vehicle_type: []
    }
  },
  created() {
    this.fetchVehicle_type()
  },
  methods: {
    async fetchVehicle_type() {
      let response = await this.$api.get('items/vehicle_type')
      this.vehicle_type = response.data.data

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
