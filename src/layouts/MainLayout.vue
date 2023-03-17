<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />
        <q-toggle :color="$q.dark.isActive ? 'white' : 'primary'" :model-value="$q.dark.isActive" @click="$q.dark.toggle()"/>
        <q-toolbar-title>
          Quasar App
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header>
          Essential Links
        </q-item-label>

        <EssentialLink v-for="link in essentialLinks" :key="link.title" v-bind="link" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
const linksList = [
  {
    title: 'Accounting Receipts',
    caption: '',
    icon: '',
    link: '/modules/accounting_receipts/'
  },
  {
    title: 'Accounting Settlements',
    caption: '',
    icon: '',
    link: '/modules/accounting_settlements/'
  },
  {
    title: 'Accounting Taxes',
    caption: '',
    icon: '',
    link: '/modules/accounting_taxes/'
  },
  {
    title: 'Accounts',
    caption: '',
    icon: '',
    link: '/modules/accounts/'
  },
  {
    title: 'Invoice details',
    caption: '',
    icon: '',
    link: '/modules/invoice_details/'
  },
  {
    title: 'Invoices',
    caption: '',
    icon: '',
    link: '/modules/invoices/'
  },
  {
    title: 'Items',
    caption: '',
    icon: '',
    link: '/modules/items/'
  },
  {
    title: 'Organisation',
    caption: '',
    icon: '',
    link: '/modules/organisation/'
  },
  {
    title: 'Document Sequence',
    caption: '',
    icon: '',
    link: '/modules/document_sequence/'
  },
  {
    title: 'Contacts',
    caption: '',
    icon: '',
    link: '/modules/contacts/'
  },
  {
    title: 'Driver',
    caption: '',
    icon: '',
    link: '/modules/driver/'
  },
  {
    title: 'Vehicles',
    caption: '',
    icon: '',
    link: '/modules/vehicles/'
  },
  {
    title: 'Log book',
    caption: '',
    icon: '',
    link: '/modules/log_book/'
  },
  {
    title: 'Contracts',
    caption: '',
    icon: '',
    link: '/modules/contracts/'
  },
  {
    title: 'Vehicle type',
    caption: '',
    icon: '',
    link: '/modules/vehicle_type/'
  },
  {
    title: 'Banks',
    caption: '',
    icon: '',
    link: '/modules/banks/'
  },
]
export default defineComponent({
  name: 'MainLayout',
  components: {
    EssentialLink
  },
  setup () {
    const leftDrawerOpen = ref(false)
    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
