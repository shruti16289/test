<template>
  <div class="q-pa-md">
    <div>
      <h5>organisation</h5>
    </div>

    <q-table separator="horizontal" :columns="table.columns" :rows="table.rows">
     <template v-slot:body-cell-mobile_number="props">
      <q-td>
      <q-btn v-if="props.value" flat icon="phone" color="primary" type="a" :label="props.value" :href="'tel:' +props.value "></q-btn>
      </q-td>
     </template>

    </q-table>
</div>
</template>

<script>


export default {
  data () {
    return {
      table: {
        rows: [

        ],
        columns: [
        { label: 'id', field: 'id' },
        { label: 'organization name', field: 'organisation_name' },
        { label: 'prefix', field: 'prefix' },
        { label: 'description', field: 'description' },
        { label: 'address', field: 'address' },
        { label: 'city', field: 'city' },
        { label: 'state', field: 'state' },
        { label: 'pin code', field: 'pin_code' },
        { label: 'contact number', field: 'contact_number' },
        { label: 'email', field: 'email' },
        { label: 'gst', field: 'gst_number' },
        { label: 'pan_no.', field: 'pan_no' },
        { label: 'invoices', field: 'invoices' },
        { label: 'status', field: 'status' },
        { label: 'user created', field: 'user_created' },
        { label: 'date created', field: 'date_created' },
        { label: 'user updated', field: 'user_updated' },
        { label: 'date updated', field: 'date_updated' },
        { label: 'banks', field: 'banks' },

        ]
      }
    }
  },

  methods: {
    insertData (data) {

      this.table.rows.push(data)
    },
     async fetchData(){
      let response =await this.$api.get('https://gangotri-api.brainysoftwares.com/items/organisation?fields=*.*')
      this.table.rows=response.data.data
      }
    },
    created(){


      this.fetchData()
    }
    }



</script>
