<template>
  <v-data-table
    :headers="headers"
    :items="numberSequence"
    :items-per-page="5"
    class="elevation-1"
  >
    <template #[`item.actions`]="{ item }">
      <v-btn>
        {{ item.name }}
      </v-btn>
      <v-btn>
        {{ item.address }}
      </v-btn>
    </template>
    <template #[`item.name`]="{ item }">
      {{ item.name }} addon
    </template>
    <template #[`item.numberSq`]="{index}">
      {{ index+1 }}
    </template>
  </v-data-table>
</template>

<script>
export default {
  data () {
    return {
      headers: [
        {
          text: 'number',
          align: 'start',
          sortable: false,
          value: 'numberSq'
        },
        { text: 'Name', value: 'name' },
        { text: 'Address', value: 'address' },
        { text: 'City', value: 'city' },
        { text: 'Pin Code', value: 'pinCode' },
        { text: 'Country', value: 'country' },
        { text: 'Actions', value: 'actions' }
      ],
      numberSequence: [
        {
          name: 'Shomas Hardy',
          address: '89 Chiaroscuro Rd.',
          city: 'Portland',
          pinCode: 97219,
          country: 'USA'
        },
        {
          name: 'Thomas Hardy',
          address: '89 Chiaroscuro Rd.',
          city: 'Portland',
          pinCode: 57219,
          country: 'USA'
        }
      ]
    }
  }
}
</script>
