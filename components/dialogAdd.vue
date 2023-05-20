<template>
  <div>
    <v-dialog
      v-model="isDialogOpen"
      max-width="398px"
    >
      <v-card light>
        <v-card-title
          style="font-size:25px; height:77px"
        >
          {{ action }} Employee <!--Fill title Text here-->
          <v-spacer />
          <v-btn
            text
            @click="isDialogOpen=false"
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
                  v-model="formInput.name"
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
                  v-model="formInput.email"
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
                  v-model="formInput.address"
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
                  v-model="formInput.phone"
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
        <v-btn text @click="isDialogOpen=false">
          <div style="color:black">
            Cancel
          </div>
        </v-btn>
        <v-btn color="primary" @click="onSubmit">
          Save
        </v-btn>
      </v-toolbar>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {

    itemTemp: {
      type: Object,
      default: null
    },
    title: {
      type: String,
      required: true
    },
    isOpen: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    formInput: {},
    inputTemp: {
      name: '',
      email: '',
      address: '',
      phone: ''
    }
  }),
  computed: {
    action: function () {
      return this.itemTemp ? 'Edit' : 'Add'
    },
    isDialogOpen: {
      get () {
        return this.isOpen
      },
      set (newValue) {
        this.$emit('dialogClose', newValue)
      }
    }
  },
  watch: {
    itemTemp: function () {
      this.checkUpdate()
    }
  },
  methods: {
    onSubmit () {
      this.$emit('onSubmit', this.action, this.formInput)
      this.isDialogOpen = false
      this.formInput = JSON.parse(JSON.stringify(this.inputTemp))
    },
    checkUpdate () {
      if (this.itemTemp) {
        this.formInput = JSON.parse(JSON.stringify(this.itemTemp))
      } else {
        this.formInput = JSON.parse(JSON.stringify(this.inputTemp))
      }
    }
  }
}
</script>
