<template>
  <v-form>
    <v-container>
    <v-card class="mb-12">
      <v-card-title class="d-block pa-2 grey darken-3 white--text" align="center">{{$t('register_list_page.title')}}</v-card-title>
      <v-container fluid class="white">
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
                :label="$t('register_list_page.status')"
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
              class="mx-auto"
            >
              <template v-slot:item.comp_id="{ item }">
                <v-row v-for="list in comp_data" :key="list.comp_id">
                  <v-col v-if="item.comp_id === list.comp_id">
                    {{ list.comp_name }}
                  </v-col>
                </v-row>
              </template>

              <template v-slot:item.action="{ item }">
                <v-icon @click="getItem(item)" color="warning" 
                v-if="item.com_regi_status_id === 0">
                  mdi-check-decagram
                </v-icon>
                <v-icon @click="getItem(item)" color="primary"
                v-else>
                  mdi-eye
                </v-icon>
              </template>
            </v-data-table>
          </v-card>

        <v-dialog v-model="loadDialog" persistent width="300">
          <v-card color="primary" dark>
            <v-card-text>
              {{ $t('loading') }}
              <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
            </v-card-text>
          </v-card> 
        </v-dialog>
      </v-container>
    </v-card>
    </v-container>
  </v-form>
</template>

<script>
const axios = require('axios')

export default {
  name: 'Staff-Register-List',
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
      status_data: [],
      comp_data: [],
      register_data: [],
      master_register_data: []
    }
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
        if (localUser.type === 'admin') {
          this.loadDialog = true
          axios.get('https://us-central1-laos-single-window.cloudfunctions.net/function/getCompanyregister')
          .then(async res => {
            this.status_data = res.data.status_data
            this.master_register_data = res.data.comp_regis_data
            this.comp_data = res.data.comp_data
            for (let i = 0; i < this.master_register_data.length; i++) {
              if (this.master_register_data[i].com_regi_status_id === 0) {
                this.register_data.push(this.master_register_data[i])
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
        {text: this.$t('register_list_page.header.no'), aligh: 'left', sortable: true, value: 'index'},
        {text: this.$t('register_list_page.header.app_id'), aligh: 'left', sortable: true, value: 'com_regi_id'},
        {text: this.$t('register_list_page.header.comp_name'), aligh: 'left', sortable: true, value: 'comp_name'},
        {text: this.$t('register_list_page.header.status'), aligh: 'left', sortable: false, value: 'status'},
        {text: this.$t("action"), align: 'center', sortable: false, value: 'action'}
      ]
    },
    itemsWithIndex() {
      return this.register_data.map(
        (register_data, index) => ({
          ...register_data,
          index: index + 1,
          comp_name: this.getCompName(register_data),
          status: this.getRegiStatus(register_data)
        })
      )
    }
  },
  methods: {
    getItem (value) {
      this.$router.push(`staff_register_approve/${value.comp_id}`)
    },
    async selectStatus (value) {
      this.register_data = []
      await this.getRegisterData(value.id)
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
        if (value.com_regi_status_id === this.status_data[index].com_regi_status_id) {
          return this.status_data[index].com_regi_status_name
        }
      }
    },
    getRegisterData (index) {
      if (index === -1) {
        this.register_data = this.master_register_data
      } else {
        let data = []
        for (let i = 0; i < this.master_register_data.length; i++) {
          if (this.master_register_data[i].com_regi_status_id === index) {
            data.push(this.master_register_data[i])
          }
        }
        this.register_data = data
      } 
    }
  }
}
</script>
