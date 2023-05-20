<template>
  <div>
    <v-data-table
      v-model="selected"
      light
      :headers="headers"
      :items="info"
      :items-per-page="5"
      show-select
      class="elevation-1"
      item-key="name"
    >
      <!--Table-data No. ++-->
      <template #[`item.numberSq`]="{index}">
        {{ index+1 }}
      </template>
      <!--create toolbar at top-->
      <template #top>
        <v-toolbar flat color="#0D47A1">
          <v-container>
            <v-row>
              <v-col
                cols="5"
              >
                <v-toolbar-title>
                  <div
                    style="color:white;"
                  >
                    Manage
                    <b>Employees</b>
                  </div>
                </v-toolbar-title>
              </v-col>
              <v-col
                cols="7"
                align="end"
              >
                <v-btn
                  class="white--text"
                  color="red"
                  @click="openDialogSelectedDelete"
                >
                  <v-icon>
                    mdi-minus-circle
                  </v-icon>
                  DELETE
                </v-btn>
                <v-btn
                  class="white--text"
                  color="green"
                  @click="openDialogAdd(null)"
                >
                  <v-icon>mdi-plus-circle</v-icon>
                  ADD NEW EMPLOYEE
                </v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-toolbar>
      </template>

      <template #[`item.actions`]="{item,index}">
        <!--Edit button-->
        <v-btn
          x-small
          text
          @click="openDialogAdd(item, index)"
        >
          <v-icon color="yellow" small>
            mdi-pencil
          </v-icon>
        </v-btn>
        <!--Delete button-->
        <v-btn
          x-small
          text
          @click="openDialogDelete(index)"
        >
          <v-icon color="red" small>
            mdi-delete
          </v-icon>
        </v-btn>
      </template>
    </v-data-table>
    <v-snackbar
      v-model="snackbar"
    >
      {{ text }}
      <template #action="{ attrs }">
        <v-btn
          color="pink"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
    <!--Dialogs-->
    <!--Call dialogAdd from components(AddEmployee,Edit)-->
    <cpn-dialog-add
      :item-temp="infoTemp"
      :is-open="dialogAdd"
      title="Add New Employee"
      @dialogClose="closeDialogAdd"
      @onSubmit="onSubmit"
    />
    <!--Call dialogDelete from components(SelectedDelete)-->
    <cpn-dialog-delete
      :is-open="dialogSelectedDelete"
      single-or-multi
      :selected="selected"
      @dialogConfirm="confirmDialogSelectedDelete"
      @dialogClose="closeDialogSelectedDelete"
    />
    <!--Call dialogDelete from components (DeleteAnEmployee)-->
    <cpn-dialog-delete
      :is-open="dialogDelete"
      :selected="selected"
      @dialogConfirm="confirmDialogDelete"
      @dialogClose="closeDialogDelete"
    />
  </div>
</template>

<script>
import employeeInfo from '../assets/data/employeeInfo.json'
import cpnDialogAdd from '../components/dialogAdd.vue'
import cpnDialogDelete from '../components/DialogDelete.vue'

export default {
  components: {
    cpnDialogAdd, cpnDialogDelete
  },
  data: () => ({
    snackbar: false,
    text: '',
    count: 0,
    infoTemp: null,
    indexTemp: -1,
    selected: [],
    dialogAdd: false,
    dialogSelectedDelete: false,
    dialogEdit: false,
    dialogDelete: false,
    info: employeeInfo,
    headers: [
      {
        text: 'No.',
        align: 'start',
        sortable: false,
        value: 'numberSq'
      },
      { text: 'Name', value: 'name' },
      { text: 'email', value: 'email' },
      { text: 'Address', value: 'address' },
      { text: 'Phone', value: 'phone' },
      { text: 'Actions', value: 'actions', sortable: false }
    ]
  }),

  methods: {
    openDialogAdd (item, index) {
      this.indexTemp = index
      this.infoTemp = item
      this.dialogAdd = true
    },
    openDialogSelectedDelete () {
      this.dialogSelectedDelete = true
    },
    openDialogDelete (index) {
      this.indexTemp = index
      this.dialogDelete = true
    },
    confirmDialogSelectedDelete () {
      if (this.selected === []) {
        this.text = 'Please Select row to delete'
        this.snackbar = true
      }
      for (let i = 0; i < this.selected.length; i++) {
        console.log(this.info.indexOf(this.selected[i]))
        this.info.splice(this.info.indexOf(this.selected[i]), 1)
      }
      this.text = 'Selection Deleted'
      this.snackbar = true
      this.selected = []
    },
    confirmDialogDelete () {
      this.text = 'Deleted'
      this.snackbar = true
      if (this.indexTemp === -1) { return }
      this.info.splice(this.indexTemp, 1)
      this.indexTemp = -1
    },
    closeDialogAdd () {
      this.dialogAdd = false
    },
    closeDialogSelectedDelete () {
      this.dialogSelectedDelete = false
    },
    closeDialogEdit () {
      this.dialogEdit = false
    },
    closeDialogDelete () {
      this.dialogDelete = false
    },
    onSubmit (action, data) {
      if (action === 'Add') {
        this.info.push(data)
        this.text = 'Added Employee'
      } else {
        this.info[this.indexTemp] = data
        const temp = this.info
        this.info = []
        setTimeout(() => {
          this.info = temp
        }, 0)
        this.text = 'Edited Employee'
      }
      this.snackbar = true
      this.indexTemp = -1
    }
  }
}
</script>

<style>
.footerFont {
  font-size: 12px;
}
.footerButton {
  width: 30px;
  height: 30px;
  min-width: 30px;
  min-height: 30px;
}
</style>
