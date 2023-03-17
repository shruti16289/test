<template>
  <q-card class="q-pa-md   scroll" style="height: 580px">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >

      <q-input ref="inputRef" v-model="formData.item_name" mask="S" type="char" reverse-fill-mask label="Item Name *" :rules="[val => !!val || 'Field is required']" />
      <q-select   clearable v-model="formData.item_type" label="Item type" :options="['Service','Service with rate']" />
      <q-select   clearable v-model="formData.status" label="Status" :options="['Public','Draft','Archieved']" />
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
