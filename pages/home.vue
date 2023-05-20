<template>
  <v-app>
    <v-card width="300" class="mx-auto mt-5">
      <v-card-title>
        <h1 class="display-1">
          Login
        </h1>
      </v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field label="Username" prepend-icon="mdi-account-circle" />
          <v-text-field type="password" label="Password" prepend-icon="mdi-lock" />
        </v-form>
      </v-card-text>
      <v-divider />
      <div style="margin-left: 10px;">
        <v-btn color="success" class="mr-2">
          Login
        </v-btn>
        <v-btn color="info">
          Register
        </v-btn>
      </div>
    </v-card>
  </v-app>
</template>

<style>
.full-image {
  object-fit: contain;
}
</style>
