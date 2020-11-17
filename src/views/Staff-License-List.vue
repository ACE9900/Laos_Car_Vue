<template>
  <v-form>
    <v-container>
    <v-card class="mb-12">
      <v-card-title class="d-block pa-2 grey darken-3 white--text" align="center">{{$t('company_license_list_page.license_list')}}</v-card-title>
        <v-container fluid>
          <v-row class="align-center">
            <v-col cols="12" xs="12" sm="8" md="8" lg="8">
              <v-text-field
              v-model="search"
              append-icon="mdi-search"
              :label="$t('register_list_page.search_text')"
              single-line
              dense
              filled
              ></v-text-field>
            </v-col>
            <v-col class="mb-6 justify-end" cols="2" xs="2" sm="1" md="1" lg="1">
              <v-row class="justify-end">
                {{ $t('register_list_page.status') }}
              </v-row> 
            </v-col>
            <v-col cols="10" xs="10" sm="3" md="3" lg="3">
              <v-select
              :label="$t('register_list_page.header.status')"
              v-model="select_status"
              :items="search_status"
              item-text="title"
              return-object
              single-line
              dense
              @input="selectStatus"
              filled
              ></v-select>
            </v-col>
          </v-row>

          <v-card :elevation="5">
            <v-data-table 
            :search="search"
            :headers="headers"
            :items="itemsWithIndex"
            :items-per-page="10"
            class="mx-auto elevation-1"
            >
              <template v-slot:item.action="{ item }">
                <v-icon @click="getItem(item)" color="warning" 
                v-if="item.app_status_id === 0 || item.app_status_id === 2">  
                  mdi-check-decagram
                </v-icon>
                <v-icon @click="getItem(item)" color="primary"
                v-else>
                  mdi-eye
                </v-icon>
              </template>
            </v-data-table>
          </v-card>
        </v-container>
      </v-card>
    </v-container>

    <v-dialog v-model="loadDialog" persistent width="300">
      <v-card color="primary" dark>
        <v-card-text>
          {{ $t('loading') }}
          <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-form>
</template>

<script>
const axios = require("axios")

export default {
  data() {
    return {
      loadDialog: false,
      search: '',
      select_status: {id: 0, title: 'Wait'},
      search_status: [
        // {id: -1, title: 'All'},
        // {id: 0, title: 'Wait'},
        // {id: 1, title: 'Accept'},
        // {id: 2, title: 'Reject'}
        {id: -1, title: 'ທັ້ງໝົດ'},
        {id: 0, title: 'ລໍອະນຸມັດ'},
        {id: 1, title: 'ອະນຸມັດ'},
        {id: 2, title: 'ປະຕິເສດ'}
      ],
      master_license_list: [],
      license_list: [],
      status_data: [],
      comp_data: []
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
        this.$router.replace({ name: "Login" })
      } else {
        if (localUser.type === 'staff' || localUser.type === "admin") {
          this.loadDialog = true
          axios.get('https://us-central1-laos-single-window.cloudfunctions.net/function/staff/licence')
          .then(res => {
            this.master_license_list = res.data.licence_data
            this.status_data = res.data.status_data
            this.comp_data = res.data.comp_data
            for (let i = 0; i < this.master_license_list.length; i++) {
              if (this.master_license_list[i].app_status_id === 0) {
                this.license_list.push(this.master_license_list[i])
              }
            }
            this.loadDialog = false
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
  computed: {
    headers () {
      return [ 
        { text: this.$t('staff_licence_list.table_header.license_no'), sortable: false, value: 'index' },
        { text: this.$t('staff_licence_list.table_header.license_number'), sortable: false, value: 'app_id' },
        { text: this.$t('staff_licence_list.table_header.request_date'), sortable: false, value: 'app_date_req' },
        { text: this.$t('staff_licence_list.table_header.company_id'), sortable: false, value: 'comp_name' },
        { text: this.$t('staff_licence_list.table_header.status'), sortable: false, value: 'status' },
        { text: this.$t("action"), align: 'center', sortable: false, value: 'action' }
      ]
    },
    itemsWithIndex() {
      return this.license_list.map(
        (license_list, index) => ({
          ...license_list,
          index: index + 1,
          comp_name: this.getCompName(license_list),
          status: this.getRegiStatus(license_list)
        })
      )
    }
  },
  methods: {
    async getItem (value) {
      this.$router.push(`/staff-license-approve/${value.app_id}`)
    },
    getCompName (value) {
      for (let index = 0; index < this.comp_data.length; index++) {
        if (value.comp_id === this.comp_data[index].comp_id) {
          return this.comp_data[index].comp_name
        }
      }
    },
    getRegiStatus (value) {
      for (let index = 0; index < this.status_data.length; index++) {
        if (value.app_status_id === this.status_data[index].app_status_id) {
          return this.status_data[index].app_status_name
        }
      }
    },
    async selectStatus (value) {
      this.license_list = []
      await this.getRegisterData(value.id)
    },
    getRegisterData (index) {
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
  }
}
</script>