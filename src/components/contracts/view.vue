<template>
  <div class="q-pa-md">
    <div>
      <h5>contracts</h5>
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
        { label: ' name', field: 'name' },
        { label: 'Account ', field: 'account' },
        { label: 'vehicle type', field: 'vehicle_type' },
        { label: 'rent', field: 'rent_per_month' },
        { label: 'fuel', field: 'fuel' },
        { label: 'date created', field: 'date_created' },
        { label: 'date updated', field: 'date_updated' },
        { label: 'log_book', field: 'log_book' },
        { label: 'is tax included' ,field: 'is_tax_included' },

        ]
      }
    }
  },

  methods: {
    insertData (data) {

      this.table.rows.push(data)
    },
     async fetchData(){
      let response =await this.$api.get('https://gangotri-api.brainysoftwares.com/items/contracts?fields=*.*')
      this.table.rows=response.data.data
      }
    },
    created(){


      this.fetchData()
    }
    }



</script>
