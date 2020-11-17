<template>
  <v-container fluid class="mb-12 white">
    <v-card-title class="d-block pa-2 grey darken-3 white--text" align="center">{{$t('register_submit_page.register_detail')}}</v-card-title>
    <v-card class="pt-1 elevation-10">
      <v-form ref="form" v-model="valid" class="px-3 mt-8">
        <v-layout row wrap align-center class="mx-1">

          <v-flex xs12 sm12 md12 lg12 no-gutters>
            <v-row dense class="px-2 align-center">
              <v-col cols="12" xs="12" sm="12" md="8" lg="8" class="px-1">
                <v-text-field
                  v-model="contact_name"
                  :label="$t('register_submit_page.contact_name_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4">
                <v-text-field
                  v-model="contact_tel"
                  :label="$t('register_submit_page.contact_tel_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
            </v-row>
          </v-flex>

          <v-flex xs12 sm12 md12 lg12 no-gutters>
            <v-row dense class="px-2 align-center">
              <v-col cols="12" xs="12" sm="12" md="8" lg="8" class="px-1">
                <v-text-field
                  v-model="company_name"
                  :label="$t('register_submit_page.company_name_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4">
                <v-text-field
                  v-model="company_code"
                  :label="$t('register_submit_page.company_code_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
            </v-row>
          </v-flex>

          <v-flex xs12 sm12 md12 lg12 no-gutters>
            <v-row dense class="px-2 align-center">
              <v-col cols="12" xs="12" sm="12" md="4" lg="4" class="px-1">
                <v-text-field
                  v-model="tax_number"
                  :label="$t('register_submit_page.tax_number_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4">
                <v-text-field
                  v-model="country"
                  :label="$t('register_submit_page.country_select')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4" class="px-1">
                <v-text-field
                  v-model="province"
                  :label="$t('register_submit_page.province_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
            </v-row>
          </v-flex>

          <v-flex xs12 sm12 md12 lg12 no-gutters>
            <v-row dense class="px-2 align-center">
              <v-col cols="12" xs="12" sm="12" md="4" lg="4" class="px-1">
                <v-text-field
                  v-model="district"
                  :label="$t('register_submit_page.district_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4">
                <v-text-field
                  v-model="village"
                  :label="$t('register_submit_page.village_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4" class="px-1">
                <v-text-field
                  v-model="address"
                  :label="$t('register_submit_page.address_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
            </v-row>
          </v-flex>

          <v-flex xs12 sm12 md12 lg12 no-gutters class="mb-5">
            <v-row dense class="px-2 align-center">
              <v-col cols="12" xs="12" sm="12" md="4" lg="4" class="px-1">
                <v-text-field
                  v-model="tel"
                  :label="$t('register_submit_page.tel_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4">
                <v-text-field
                  v-model="fax"
                  :label="$t('register_submit_page.fax_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
              <v-col cols="12" xs="12" sm="12" md="4" lg="4" class="px-1">
                <v-text-field
                  v-model="email"
                  :label="$t('register_submit_page.email_field')"
                  hide-details
                  filled
                  readonly
                ></v-text-field>
              </v-col>
            </v-row>
          </v-flex>

          <div class style="width: 100%">
            <v-divider class="black"></v-divider>
            <div class="title text-center py-2">
              <h3>{{ $t('register_submit_page.staff_title_text') }}</h3>
            </div>
            <v-divider class="black"></v-divider>

            <v-flex xs12 sm12 md12 lg12 no-gutters class="mt-4">
              <v-row dense class="px-2 align-center">
                <v-col cols="12" xs="12" sm="12" md="4" lg="4" class="px-1">
                  <v-select
                  v-if="!isApprove" 
                  :label="$t('register_submit_page.staff_status_select')"
                  v-model="status_select"
                  :rules="[rules.status]"
                  :items="status"
                  item-text="com_regi_status_name"
                  item-value="status_id"
                  persistent-hint
                  return-object
                  single-line
                  :readonly="isApprove"
                  @change="statusSelect"
                  filled></v-select>

                  <v-text-field
                    v-else
                    :label="$t('register_submit_page.staff_status_select')"
                    v-model="status_select.com_regi_status_name"
                    :readonly="isApprove"
                    filled
                  ></v-text-field>
                </v-col>
                <v-col v-if="showNote" cols="12" xs="12" sm="12" md="8" lg="8" class="px-1">
                  <v-text-field
                    :label="$t('register_submit_page.staff_note_field')"
                    :rules="[rules.require]"
                    v-model="note"
                    :readonly="isApprove"
                    filled
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-flex>
            <v-dialog v-model="confirmDialog" persistent max-width="290">
              <template v-slot:activator="{ on }">
                <v-row v-if="!isApprove" class="px-8 justify-end mb-4">
                  <v-btn :disabled="!valid" min-width="200" class="success" v-on="on">{{ $t('register_submit_page.submit_button') }}</v-btn>
                </v-row>
              </template>
              <v-card>
                <v-card-title class="headline">{{ $t('confirm_dialog.title') }}</v-card-title>
                <v-card-text>{{ $t('confirm_dialog.text') }}</v-card-text>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="red darken-4" text @click="confirmDialog = false">{{ $t('confirm_dialog.cancel_btn') }}</v-btn>
                  <v-btn color="green darken-4" text @click="submit">{{ $t('confirm_dialog.confirm_btn') }}</v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </div>
        </v-layout>
      </v-form>
    </v-card>
    
    <v-dialog
      v-model="dialog"
      hide-overlay
      persistent
      width="300"
    >
      <v-card color="primary" dark>
        <v-card-text> 
          {{ $t('loading') }}
          <v-progress-linear
            indeterminate
            color="white"
            class="mb-0"
          ></v-progress-linear>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
const axios = require("axios")

export default {
  name: "Staff-Register-submit",

  data () {
    return {
      confirmDialog: false,
      isApprove: false,
      showNote: false,
      dialog: false,
      valid: false,
      contact_name: '',
      contact_tel: '',
      company_name: '',
      company_code: '',
      tax_number: '',
      country: '',
      province: '',
      district: '',
      village: '',
      address: '',
      tel: '',
      fax: '',
      email: '',
      status: [],
      status_select: {com_regi_status_id: 0, com_regi_status_name: 'wait'},
      note: null,
      rules: {
        require: value => !!value || 'required',
        status: value => value.com_regi_status_id !== 0 || 'required'
      }
    }
  },
  beforeCreate() {
    this.$store.dispatch("currentPage/setCurrentPage", this.$route.name)
  },
  created() {
    let localUser = localStorage.getItem('localUser')
    localUser = JSON.parse(localUser)
    try {
      if (localUser === null || localUser === undefined) {
        this.$router.replace({ name: "Login" })
      } else {
        if (localUser.type === 'admin') {
          this.dialog = true
          let comp_id = this.$route.params.id
          axios.get(`https://us-central1-laos-single-window.cloudfunctions.net/function/getCompanyregister/${comp_id}`)
          .then(res => {
            this.setData(res.data)
          })
          .catch(err => {
            console.log(err)
          })
        } else {
          localStorage.clear()
          this.$router.replace({ name: "Login" })
        }
      }
    } catch {
      localStorage.clear()
      this.$router.replace({ name: "Login" })
    }
  },
  methods: {
    setData (data) {
      if (data.comp_regi_data.com_regi_status_id !== 0) {
        this.isApprove = true
        this.status_select.com_regi_status_id = data.comp_regi_data.com_regi_status_id
        if (data.comp_regi_data.com_regi_status_id === 1) {
          this.status_select.com_regi_status_name = 'accept'
        } else {
          this.status_select.com_regi_status_name = 'reject'
        }
        this.note = data.comp_regi_data.com_regi_note
      }
      this.contact_name = data.comp_data.comp_contact_name
      this.contact_tel = data.comp_data.comp_contact_tel
      this.company_name = data.comp_data.comp_name
      this.company_code = data.comp_data.comp_code
      this.tax_number = data.comp_data.comp_taxnumber
      this.country = data.comp_data.comp_country
      this.province = data.comp_data.comp_province
      this.district = data.comp_data.comp_district
      this.village = data.comp_data.comp_village
      this.address = data.comp_data.comp_address
      this.tel = data.comp_data.comp_tel
      this.fax = data.comp_data.comp_fax
      this.email = data.comp_data.comp_email
      this.status = data.status_data
      this.dialog = false
    },
    async submit () {
      this.dialog = true
      const localUser = JSON.parse(localStorage.getItem('localUser'))
      let comp_id = this.$route.params.id
      await axios.post('https://us-central1-laos-single-window.cloudfunctions.net/function/updateCompany', {
        comp_id: Number(comp_id),
        email: this.email,
        contact_name: this.contact_name,
        comp_name: this.company_name,
        staff: localUser.username,
        note: this.note,
        status: this.status_select.com_regi_status_id
      })
      .then(res => {
        console.log(res)
        this.dialog = false
        this.$router.replace( { name: 'Staff-Register-List' } )
      })
      .catch(err => {
        console.log(err)
      })
    },
    statusSelect () {
      if (this.status_select.com_regi_status_id === 2) {
        this.showNote = true
      } else {
        this.showNote = false
        this.note = null
      }
    }
  }
};
</script>
