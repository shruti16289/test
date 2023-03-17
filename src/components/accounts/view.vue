<template>
  <div class="q-pa-md">
    <div>
      <h5>accounts</h5>
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
        { label: 'Account name', field: 'account_name' },
        { label: 'Account address', field: 'account_address' },
        { label: 'Contact number', field: 'contact_number' },
        { label: 'email', field: 'email' },
        { label: 'city', field: 'city' },
        { label: 'state', field: 'state' },
        { label: 'pin code', field: 'pin_code' },
        { label: 'country', field: 'country' },
        { label: 'account recepit', field: 'account_recepit' },
        { label: 'status', field: 'status' },
        { label: 'user created', field: 'user_created' },
        { label: 'date created', field: 'date_created' },
        { label: 'user updated', field: 'user_updated' },
        { label: 'date updated', field: 'date_updated' },
        { label: 'invoices', field: 'invoices' },
        { label: 'contacts', field: 'contacts' },
        { label: 'log book', field: 'log_book' },
        { label: 'contracts', field: 'contracts' },
        { label: 'gst', field: 'gst' },
        ]
      }
    }
  },

  methods: {
    insertData (data) {

      this.table.rows.push(data)
    },
     async fetchData(){
      let response =await this.$api.get('https://gangotri-api.brainysoftwares.com/items/accounts?fields=*.*')
      this.table.rows=response.data.data
      }
    },
    created(){


      this.fetchData()
    }
    }



</script>
