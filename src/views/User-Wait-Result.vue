<template>
    <v-container fluid class="white">
      <v-card max-width="50%" class="pb-6 mt-12 mx-auto elevation-10">
        <!-- Header Text -->
        <v-card-title class="headline d-block pa-2 grey darken-3 white--text" align="center">{{ $t('register_page.confirm_register_title') }}</v-card-title>
          <v-row dense class="px-2 align-center">
            <!-- Image Correct -->
            <v-row align="center" justify="center">
              <v-img class="mt-5" max-width="20%" contain src="../assets/check-mark.png"></v-img>
            </v-row>
            <!-- Text -->
            <v-card-text class="my-4 subtitle-1" align="center" justify="center">
              {{ $t('register_page.confirm_register_text') }}
            </v-card-text>
            <!-- Button -->
            <v-card-actions class="mx-auto">
              <v-spacer></v-spacer>
              <v-btn color="blue white--text" @click="toLogin">{{ $t('register_page.confirm_register_button') }}</v-btn>
            </v-card-actions>
          </v-row>
      </v-card>
    </v-container>
</template>

<script>
export default {
  data: () => ({

  }),
  methods: {
    toLogin () {
        this.$router.replace({ name: 'Login' })
    }
  }
}
</script>
