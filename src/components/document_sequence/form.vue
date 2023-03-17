<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-input v-model="formData.date_created"  label="Date created" />
      <q-select clearable v-model="formData.organisation_id" label="Organisation ID"
      :options="organisation" option-label="id" type="char" option-value="organisation_name" map-options emit-value />
      <q-select ref="inputRef" clearable v-model="formData.document_type" type="char" label="Document Type*" :options="['Invoice','Receipt']" :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.sequence_no" label="Sequence no" />
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


