<template>
  <div>
    <v-dialog
      v-model="isDialogOpen"
      max-width="500px"
    >
      <v-card light>
        <v-card-title>
          <div style="font-size:24px">
            Delete Employees
          </div>
          <v-spacer />
          <v-btn text @click="isDialogOpen=false">
            <v-icon>
              mdi-close
            </v-icon>
          </v-btn>
        </v-card-title>
        <v-divider />
        <v-card flat>
          <v-col>
            <v-card-text style="width:338px; height:21px;margin-bottom:16px">
              <div style="font-size:14px;">
                Are you sure you want to delete these Records?
              </div>
            </v-card-text>
            <v-card-text>
              <div style="color:#d4e157;">
                this action cannot be undone.
              </div>
            </v-card-text>
          </v-col>
        </v-card>
        <v-divider />
        <v-toolbar bottom color="grey lighten-2">
          <v-card />
          <v-spacer />
          <v-card-actions>
            <v-spacer />
            <v-btn
              text
              color="black"
              @click="isDialogOpen = false"
            >
              Cancel
            </v-btn>
            <v-btn
              color="red"
              @click="confirmDelete"
            >
              <div style="color: white">
                Delete
              </div>
            </v-btn>
          </v-card-actions>
        </v-toolbar>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    isOpen: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
  }),
  computed: {
    isDialogOpen: {
      get () {
        return this.isOpen
      },
      set (newValue) {
        this.$emit('dialogClose', newValue)
      }
    }
  },
  methods: {
    confirmDelete () {
      this.isDialogOpen = false
      this.$emit('dialogConfirm')
      console.log('test')
    }
  }
}
</script>
