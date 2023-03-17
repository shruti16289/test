<template>
  <div class="q-pa-md">
    <div>
      <h5>items</h5>
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
  data() {
    return {
      table: {
        rows: [

        ],
        columns: [
        { label: 'id', field: 'id' },
        { label: 'item name', field: 'item_name' },
        { label: 'item type', field: 'item_type' },
        { label: 'status', field: 'status' },
        { label: 'user created', field: 'user_created' },
        { label: 'date created', field: 'date_created' },
        { label: 'user updated', field: 'user_updated' },
        { label: 'date updated', field: 'date_updated' },

        ]
      }
    }
  },

  methods: {
    insertData (data) {

      this.table.rows.push(data)
    },
     async fetchData(){
      let response =await this.$api.get('https://gangotri-api.brainysoftwares.com/items/items?fields=*.*')
      this.table.rows=response.data.data
      }
    },
    created(){


      this.fetchData()
    }
    }



</script>
