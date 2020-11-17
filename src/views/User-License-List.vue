<template>
  <v-form>
    <v-container class="mb-12">
      <v-card min-height="485">
        <v-card-title class="d-block pa-2 grey darken-3 white--text" align="center">{{$t('company_license_list_page.license_list')}}</v-card-title>
          <v-container fluid>
            <v-row class="align-center">
              <v-col cols="12" xs="12" sm="8" md="8" lg="8">
                <v-text-field
                v-model="search"
                append-icon="mdi-search"
                :label="$t('company_license_list_page.search_text')"
                hide-details
                single-line
                dense
                filled
                ></v-text-field>
              </v-col>
              <v-col class="justify-end" cols="2" xs="2" sm="1" md="1" lg="1">
                <v-row class="justify-end">
                  {{ $t('register_list_page.status') }}
                </v-row> 
              </v-col>
              <v-col cols="10" xs="10" sm="3" md="3" lg="3">
                <v-select
                :label="$t('register_list_page.header.status')"
                v-model="select_status"
                :items="get"
                item-text="title"
                return-object
                single-line
                hide-details
                dense
                @input="selectStatus"
                filled
                ></v-select>
              </v-col>
            </v-row> 
            <v-row class="justify-end pr-4">
              <v-btn class="primary" @click="toLicenceRegis">
                <v-icon>mdi-plus-circle-outline</v-icon>
              </v-btn>
            </v-row>
          </v-container>
        <v-card-subtitle>
          <!-- เอกสารแนบ / ເອກະສານຄັດຕິດ -->
          <v-card :elevation="5">
            <v-data-table 
            :headers="headers" 
            :items="itemsWithIndex" 
            :items-per-page="10" 
            :search="search"
            class="mx-auto my-2 elevation-1"
            >

            <template v-slot:item.action="{ item }">
              <v-icon @click="toLicenceDetail(item)" color="primary"
              v-if="item.app_status_id === 1">
                mdi-eye
              </v-icon>

              <v-icon @click="toLicenceDetail(item)" color="success" 
              v-if="item.app_status_id === 0 || item.app_status_id === 2 || item.app_status_id === 3">
                mdi-pencil
              </v-icon>

              <v-icon @click="deleteApp(item)" color="error" 
              v-if="item.app_status_id === 0 || item.app_status_id === 2 || item.app_status_id === 3">
                mdi-delete
              </v-icon>
            </template>

            </v-data-table>
          </v-card>
        </v-card-subtitle>
      </v-card>

      <v-dialog v-model="dialog" persistent width="300">
      <v-card :color="dialog_color" dark>
        <v-card-text>
          {{ dialog_text }}
          <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
        </v-card-text>
      </v-card>
    </v-dialog>
    <!-- Snackbar -->
    <v-snackbar v-model="snack" :timeout="2000" :color="snackColor">
      {{ snackText }}
      <v-btn icon @click="snack = false"><v-icon color="white">mdi-close</v-icon></v-btn>
    </v-snackbar>

    </v-container>
  </v-form>
</template>

<script>
const axios = require("axios")

export default {
  data() {
    return {
      snack: false,
      snackColor: '',
      snackText: '',
      dialog: false,
      search: "",
      showdetail: false,
      master_license_list: [],
      license_list: [],
      select_status: {id: -1, title: 'All'},
      app_status: [],
      get: [
        // {id: -1, title: 'All'},
        // {id: 0, title: 'Wait'},
        // {id: 1, title: 'Accept'},
        // {id: 2, title: 'Reject'}
        {id: -1, title: 'ທັ້ງໝົດ'},
        {id: 0, title: 'ລໍອະນຸມັດ'},
        {id: 1, title: 'ອະນຸມັດ'},
        {id: 2, title: 'ປະຕິເສດ'},
        {id: 3, title: 'ແບບຮ່າງ'}
      ]
    };
  },
  beforeCreate () {
    this.$store.dispatch('currentPage/setCurrentPage', this.$route.name)
  },
  created () {
    let localUser = localStorage.getItem('localUser')
    localUser = JSON.parse(localUser)
    try {
      if (localUser === null || localUser === undefined) {
        this.$router.replace({ name: 'Login' })
      } else {
        let username = localUser.username
        if (localUser.type === 'company') {
          this.dialog_text = this.$t('loading')
          this.dialog_color = 'primary'
          this.dialog = true
          axios.get(`https://us-central1-laos-single-window.cloudfunctions.net/function/user/licence/${username}`)
          .then(res => {
            this.master_license_list = res.data.licence_data
            this.license_list = res.data.licence_data
            this.app_status = res.data.status_data
            this.dialog = false
          })
          .catch(err => {
            console.log(err)
          })
        } else {
          localStorage.clear()
          this.$router.replace({ name: 'Login' })
        }
      }
    } catch {
      localStorage.clear()
      this.$router.replace({ name: 'Login' })
    }
  },
  computed: {
    headers () {
      return [
        { text: this.$t('company_license_list_page.table_header.license_no'), align: 'left', sortable: false, value: 'index' },
        { text: this.$t('company_license_list_page.table_header.license_number'), sortable: false, align: 'left', value: 'app_id' },
        { text: this.$t('company_license_list_page.table_header.request_date'), sortable: false, align: 'center', value: 'app_date_req' },
        { text: this.$t('company_license_list_page.table_header.status'), sortable: false, align: 'center', value: 'status' },
        { text: this.$t('company_license_list_page.table_header.approve_date'), sortable: false, align: 'center', value: 'app_detail_date_approve' },
        { text: this.$t('company_license_list_page.table_header.expire_date'), sortable: false, align: 'center', value: 'app_date_expire' },
        { text: this.$t("action"), sortable: false, value: 'action' }
      ]
    },
    itemsWithIndex() {
      return this.license_list.map(
        (license_list, index) => ({
          ...license_list,
          index: index + 1,
          status: this.getLicenseStatus(license_list)
        })
      )
    }
  },
  methods: {
    async selectStatus (value) {
      this.license_list = []
      await this.getLicenseData(value.id)
    },
    getLicenseData (index) {
      if (index === -1) {
        this.license_list = this.master_license_list
      } else {
        let data = []
        for (let i = 0; i < this.master_license_list.length; i++) {
          if (this.master_license_list[i].app_status_id === index) {
            data.push(this.master_license_list[i])
          }
        }
        this.license_list = data
      } 
    },
     getLicenseStatus (value) {
      for (let index = 0; index < this.app_status.length; index++) {
        if (value.app_status_id === this.app_status[index].app_status_id) {
          return this.app_status[index].app_status_name
        }
      }
    },
    toLicenceRegis () {
      this.$router.push( { name: 'User-License-Register' } )
    },
    toLicenceDetail (item) {
      this.$router.push(`/license_detail/${item.app_id}`)
    },
    async deleteApp (item) {
      const app_id = item.app_id
     
      confirm(this.$t('delete_item')) && 
      (
        this.dialog_text = this.$t('deleting'),
        this.dialog_color = 'error',
        this.dialog = true,
        await axios.post(`https://us-central1-laos-single-window.cloudfunctions.net/function/user/licence/delete/${app_id}`)
        .then(async res => {
          const index = Number(item.index) - 1
          this.license_list.splice(index, 1)
          this.snack = true
          this.snackText = this.$t("company_license_register_page.snackbar_del"),
          this.snackColor = 'error'
          this.dialog = false
        })
        .catch(err => {
          console.log(err)
        })
      )
    }
  }
}
</script>