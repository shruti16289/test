<template>
  <div class="q-pa-md">
    <div>
      <h5>driver</h5>
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
        { label: 'driver name', field: 'driver_name' },
        { label: 'address', field: 'address' },
        { label: 'Contact number', field: 'contact_no' },
        { label: 'status', field: 'status' },

        ]
      }
    }
  },

  methods: {
    insertData (data) {

      this.table.rows.push(data)
    },
     async fetchData(){
      let response =await this.$api.get('https://gangotri-api.brainysoftwares.com/items/driver?fields=*.*')
      this.table.rows=response.data.data
      }
    },
    created(){


      this.fetchData()
    }
    }



</script>
