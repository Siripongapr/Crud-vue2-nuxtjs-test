<template>
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
    <template #[`item.numberSq`]="{index}">
      {{ index+1 }}
    </template>

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
                color="green"
                @click="openDialogAdd"
              >
                ADD NEW EMPLOYEE
              </v-btn>
              <v-btn
                color="red"
                @click="openDialogSelectedDelete"
              >
                DELETE
              </v-btn>
            </v-col>
          </v-row>
        </v-container> <!--Header text -->

        <!--Dialog ADD New Employee-->
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

        <!--Dialog Selected Delete-->
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
      </v-toolbar>
    </template>

    <template slot="item.actions">
      <v-btn
        @click="openDialogEdit"
      >
        test dialog 1
      </v-btn>
      <!--Dialog Edit-->
      <v-dialog
        v-model="dialogEdit"
        max-width="500px"
        content-class="elevation-0"
      >
        <!-- content-class is for remove shadow box -->
        <v-card>
          <v-card-title>
            Edit Employee
          </v-card-title>
          <v-divider />
          <v-container>
            <v-row>
              <v-col
                cols="12"
              >
                <v-text-field
                  label="First Name"
                  outlined
                />
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-dialog>
    </template> <!--Edit Delete dialog Icon-->
  </v-data-table>
</template>

<script>
export default {
  data: () => ({
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
