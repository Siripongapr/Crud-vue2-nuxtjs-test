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
                  @click="openDialogAdd"
                >
                  <v-icon>mdi-plus-circle</v-icon>
                  ADD NEW EMPLOYEE
                </v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-toolbar>
      </template>

      <template slot="item.actions">
        <!--Edit button-->
        <v-btn
          x-small
          text
          @click="openDialogEdit"
        >
          <v-icon color="yellow" small>
            mdi-pencil
          </v-icon>
        </v-btn>
        <!--Delete button-->
        <v-btn
          x-small
          text
          @click="openDialogDelete"
        >
          <v-icon color="red" small>
            mdi-delete
          </v-icon>
        </v-btn>
      </template>
    </v-data-table>

    <!--Dialogs-->
    <!--Dialog Add New Employee-->
    <v-dialog
      v-model="dialogAdd"
      max-width="500px"
    >
      <v-card>
        <v-card-title>Add New Employee</v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                ms="4"
              >
                <v-text-field
                  label="Name"
                  hint="Enter your Name"
                />
              </v-col>
              <v-col
                cols="12"
                sm="6"
                ms="4"
              >
                <v-text-field
                  label="Email"
                  hint="exam@gmail.com"
                />
              </v-col>
              <v-col
                cols="8"
                sm="8"
                ms="8"
              >
                <v-text-field
                  label="Address"
                />
              </v-col>
              <v-col
                cols="4"
                sm="4"
                ms="4"
              >
                <v-text-field
                  label="Phone"
                  hint="Phone number"
                />
              </v-col>
            </v-row>
          </v-container>
          <small>*please check information before confirm*</small>
        </v-card-text>

        <v-card-actions>
          <v-spacer />
          <v-btn
            color="red"
            text
            @click="dialogAdd=false"
          >
            Close
          </v-btn>

          <v-btn
            color="green"
            @click="dialogAdd=false"
          >
            Confirm
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!--Dialog SelectedDelete-->
    <v-dialog
      v-model="dialogSelectedDelete"
      max-width="500px"
    >
      <v-card>
        <v-card-title>
          <b>Delete Employees</b>
        </v-card-title>
        <v-card-text>
          <div style="font-size: 15px;">
            Confirm to delete all column
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="red"
            @click="dialogSelectedDelete = false"
          >
            Confirm
          </v-btn>
          <v-btn
            color="blue"
            @click="dialogSelectedDelete = false"
          >
            Cancel
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!--Dialog Edit-->
    <v-dialog
      v-model="dialogEdit"
      max-width="398px"
    >
      <v-card light>
        <v-card-title
          style="font-size:25px; height:77px"
        >
          Edit Employee
          <v-spacer />
          <v-btn
            text
            @click="dialogEdit=false"
          >
            <v-icon>
              mdi-close
            </v-icon>
          </v-btn>
        </v-card-title>
        <v-divider />
        <v-card style="height:396px">
          <!--Name box-->
          <v-container style="width:338px; height:67px; margin-bottom:20px">
            <v-row>
              <v-col>
                <div style="font-size:14; width:50px; height:21px; margin-bottom:10px">
                  Name
                </div>
                <v-text-field
                  style="width:338px;"
                  dense
                  label=" "
                  placeholder="Please fill your name"
                  hint="*require"
                  solo
                  flat
                  outlined
                />
              </v-col>
            </v-row>
          </v-container>

          <!--Email box-->
          <v-container style="width:338px; height:67px; margin-bottom:20px">
            <v-row>
              <v-col>
                <div style="font-size:14; width:50px; height:21px; margin-bottom:10px">
                  Email
                </div>
                <v-text-field
                  style="width:338px;"
                  dense
                  label=" "
                  placeholder="Please fill your Email"
                  hint="*require"
                  solo
                  flat
                  outlined
                />
              </v-col>
            </v-row>
          </v-container>

          <!--Address box-->
          <v-container style="width:338px; height:67px; margin-bottom:35px">
            <v-row>
              <v-col>
                <div style="font-size:14; width:70px; height:21px; margin-bottom:10px">
                  Address
                </div>
                <v-text-field
                  style="width:338px;"
                  height="62px"
                  label=" "
                  placeholder="Please fill your Address"
                  hint="*require"
                  solo
                  flat
                  outlined
                />
              </v-col>
            </v-row>
          </v-container>

          <!--Phone box-->
          <v-container style="width:338px; height:67px; margin-bottom:25px">
            <v-row>
              <v-col>
                <div style="font-size:14; width:50px; height:21px; margin-bottom:10px">
                  Phone
                </div>
                <v-text-field
                  style="width:338px;"
                  dense
                  label=" "
                  placeholder="Please fill your Phone"
                  hint="*require"
                  solo
                  flat
                  outlined
                />
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-card>
      <v-toolbar color="grey lighten-2" height="87px">
        <v-card /> <!--blank for spacer btn-->
        <v-spacer />
        <v-btn text>
          Cancel
        </v-btn>
        <v-btn color="primary">
          Save
        </v-btn>
      </v-toolbar>
    </v-dialog>
  </div>
</template>

<script>

export default {
  data: () => ({
    count: 0,
    selected: [],
    dialogAdd: false,
    dialogEdit: false,
    dialogSelectedDelete: false,

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
    ],
    info: [
      {
        name: 'Thomas Hardy',
        email: 'thomashardy@mail.com',
        address: '89 Chiaroscuro Rd, Portland, USA',
        phone: '(171) 555-2222'
      },
      {
        name: 'Dominique Perrier',
        email: 'dominiqueperrier@mail.com',
        address: 'Obere Str. 57, Berlin, Germany',
        phone: '(313) 555-5735'
      },
      {
        name: 'Maria Anders',
        email: 'dominiqueperrier@mail.com',
        address: '25, rue Lauriston, Paris, France',
        phone: '(503) 555-9931'
      },
      {
        name: 'Fran Wilson',
        email: 'franwilson@mail.com',
        address: 'C/ Araquil, 67, Madrid, Spain',
        phone: '(204) 619-5731'
      },
      {
        name: 'Martin Blank',
        email: 'martinblank@mail.com',
        address: 'Via Monte Bianco 34, Turin, Italy',
        phone: '(480) 631-2097'
      },
      {
        name: 'Martin Blank',
        email: 'martinblank@mail.com',
        address: 'Via Monte Bianco 34, Turin, Italy',
        phone: '(480) 631-2097'
      }
    ]
  }),

  methods: {
    openDialogEdit () {
      this.dialogEdit = true
    },
    openDialogAdd () {
      this.dialogAdd = true
    },
    openDialogSelectedDelete () {
      this.dialogSelectedDelete = true
    }
  }
}
</script>
