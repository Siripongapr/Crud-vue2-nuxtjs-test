<template>
  <div>
    <v-data-table
      v-model="selected"
      light
      :headers="headers"
      :items="info"
      :items-per-page="6"
      show-select
      class="elevation-1"
      item-key="name"
      hide-default-footer
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
      <template #footer>
        <v-container>
          <div class="d-flex  footerFont">
            <div
              class="mr-auto"
            >
              Showing
              <b> 5 </b>
              out of
              <b> 25 </b>
              entries
            </div>
            <div
              class="d-flex footerFont"
            >
              <v-btn text style="font-size:12px">
                Previous
              </v-btn>
              <v-btn text style="font-size:12px">
                1
              </v-btn>
              <v-btn text style="font-size:12px">
                2
              </v-btn>
              <v-btn text style="font-size:12px">
                3
              </v-btn>
              <v-btn text style="font-size:12px">
                4
              </v-btn>
              <v-btn text style="font-size:12px">
                5
              </v-btn>
              <v-btn text style="font-size:12px">
                Next
              </v-btn>
            </div>
          </div>
        </v-container>
      </template>
    </v-data-table>

    <!--Dialogs-->
    <!--Call dialogAdd from components-->
    <cpn-dialog-add
      :item-temp="itemTempo"
      :is-open="dialogAdd"
      title="Add New Employee"
      @dialogClose="closeDialogAdd"
      @onSubmit="onSubmit"
    />
    <!--Call dialogDelete from components-->
    <cpn-dialog-delete
      :is-open="dialogSelectedDelete"
      @dialogClose="closeDialogSelectedDelete"
    />

    <!--Call dialogDelete from components (reuse)-->
    <cpn-dialog-delete
      :is-open="dialogDelete"
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
    itemTempo: null,
    count: 0,
    infoTempo: -1,
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
      this.infoTempo = index
      this.itemTempo = item
      this.dialogAdd = true
    },
    openDialogSelectedDelete () {
      this.dialogSelectedDelete = true
    },
    openDialogEdit () {
      this.dialogEdit = true
    },
    openDialogDelete (index) {
      this.infoTempo = index
      this.dialogDelete = true
    },
    confirmDialogDelete () {
      if (this.infoTempo === -1) { return }
      this.info.splice(this.infoTempo, 1)
      this.infoTempo = -1
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
      } else {
        this.info[this.infoTempo] = data
        const temp = this.info
        this.info = []
        setTimeout(() => {
          this.info = temp
        }, 0)
      }
      this.infoTempo = -1
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
