<template>
  <v-container>
    <v-card class="mb-12">
      <v-card-title class="d-block pa-2 grey darken-3 white--text" align="center">{{$t('staff_logo_report.logo_header')}}</v-card-title>
      <v-tabs grow v-model="tabs" color="black" background-color="grey" active-class="amber darken-1">
        <v-tab class="font-weight-bold subtitle-1">
          {{ $t("staff_logo_report.tab_1.tab_header_1") }}
        </v-tab>
        <v-tab class="font-weight-bold subtitle-1">
          {{ $t("staff_logo_report.tab_2.tab_header_2") }}
        </v-tab>
        <v-tab class="font-weight-bold subtitle-1">
          {{ $t("staff_logo_report.tab_3.tab_header_3") }}
        </v-tab>
        <v-tab class="font-weight-bold subtitle-1">
          {{ $t("staff_logo_report.tab_4.tab_header_4") }}
        </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tabs">
      <!-- Header Logo -->
        <v-tab-item>
          <v-container>
            <v-card-title class="d-block mt-1 pa-2 grey lighten-1 black--text">
              <v-row class="mx-1 justify-space-between">
                {{ $t('staff_logo_report.tab_1.title_1.header_list') }}
                <v-btn text small class="primary" @click="headerDialog = !headerDialog">
                  <v-icon>mdi-plus-circle-outline</v-icon>
                </v-btn>
              </v-row>
            </v-card-title>
            <v-card class="mx-auto mt-3">
              <v-data-table :headers="header_doc" :items="headerWithIndex" :items-per-page="10" class="elevation-1">
                <template v-slot:item.action="{ item }">
                  <v-icon color="red" @click="deleteHeaderFile(item)">mdi-delete</v-icon>
                </template>

                <template v-slot:item.header_name="{ item }">
                  <v-row>
                    <v-col class="align-center">
                      <a @click="openHeader(item)" class="black--text">{{ showHeadername(item) }}</a>
                    </v-col>
                  </v-row>
                </template>

                <template v-slot:item.header_image="{ item }">
                  <v-img class="mx-auto ma-2" contain :src="item.header_link" width="75" height="75"/>
                </template>

                <template v-slot:item.select="{ item }">
                  <v-btn text small class="success ml-6 mb-4" @click="selectedHeader(item)">
                    <v-icon>mdi-checkbox-marked-outline</v-icon>
                  </v-btn>
                </template>

                <template v-slot:item.header_status ="{ item }">
                  <v-btn text small>
                    {{item.header_status}}
                  </v-btn>
                </template>

              </v-data-table>
            </v-card>
          </v-container>
        </v-tab-item>

      <!-- Header2 Logo -->
        <v-tab-item>
          <v-container>
            <v-card-title class="d-block mt-1 pa-2 grey lighten-1 black--text">
              <v-row class="mx-1 justify-space-between">
                {{ $t('staff_logo_report.tab_2.title_1.header2_list') }}
                <v-btn text small class="primary" @click="header2Dialog = !header2Dialog">
                  <v-icon>mdi-plus-circle-outline</v-icon>
                </v-btn>
              </v-row>
            </v-card-title>
            <v-card class="mx-auto mt-3">
              <v-data-table :headers="header2_doc" :items="header2WithIndex" :items-per-page="10" class="elevation-1">
                <template v-slot:item.action="{ item }">
                  <v-icon color="red" @click="deleteHeader2File(item)">mdi-delete</v-icon>
                </template>

                <template v-slot:item.header2_name="{ item }">
                  <v-row>
                    <v-col class="align-center">
                      <a @click="openHeader2(item)" class="black--text">{{ showHeader2name(item) }}</a>
                    </v-col>
                  </v-row>
                </template>

                <template v-slot:item.header2_image="{ item }">
                  <v-img class="mx-auto ma-2" contain :src="item.header2_link" width="75" height="75"/>
                </template>

                <template v-slot:item.select="{ item }">
                  <v-btn text small class="success ml-6 mb-4" @click="selectedHeader2(item)">
                    <v-icon>mdi-checkbox-marked-outline</v-icon>
                  </v-btn>
                </template>

                <template v-slot:item.header2_status ="{ item }">
                  <v-btn text small>
                    {{item.header2_status}}
                  </v-btn>
                </template>
              </v-data-table>
            </v-card>
          </v-container>
        </v-tab-item>

      <!-- Watermark Logo -->
        <v-tab-item>
          <!-- เอกสารแนบ / ເອກະສານຄັດຕິດ -->
          <v-card-title class="d-block mt-1 pa-2 grey lighten-1 black--text">
            <v-row class="mx-1 justify-space-between">
              {{ $t('staff_logo_report.tab_3.title_1.watermark_list') }}
              <v-btn text small class="primary" @click="watermarkDialog = !watermarkDialog">
                <v-icon>mdi-plus-circle-outline</v-icon>
              </v-btn>
            </v-row>
          </v-card-title>
          <v-card class="mx-auto mt-3">
            <v-data-table :headers="watermark_doc" :items="watermarkWithIndex" :items-per-page="10" class="elevation-1">
              <template v-slot:item.action="{ item }">
                <v-icon color="red" @click="deleteWatermarkFile(item)">mdi-delete</v-icon>
              </template>

              <template v-slot:item.watermark_name="{ item }">
                <v-row>
                  <v-col class="align-center">
                    <a @click="openWatermark(item)" class="black--text">{{ showWatermarkname(item) }}</a>
                  </v-col>
                </v-row>
              </template>

              <template v-slot:item.watermark_image="{ item }">
                <v-img class="mx-auto ma-2" contain :src="item.watermark_link" width="75" height="75"/>
              </template>

              <template v-slot:item.select="{ item }">
                <v-btn text small class="success ml-6 mb-4" @click="selectedWatermark(item)">
                  <v-icon>mdi-checkbox-marked-outline</v-icon>
                </v-btn>
              </template>

              <template v-slot:item.watermark_status ="{ item }">
                <v-btn text small>
                  {{item.watermark_status}}
                </v-btn>
              </template>

            </v-data-table>
          </v-card>
        </v-tab-item>

      <!-- Seal Logo -->
        <v-tab-item>
          <v-card-title class="d-block mt-1 pa-2 grey lighten-1 black--text">
            <v-row class="mx-1 justify-space-between">
              {{ $t('staff_logo_report.tab_4.title_1.seal_list') }}
              <v-btn text small class="primary" @click="sealDialog = !sealDialog">
                <v-icon>mdi-plus-circle-outline</v-icon>
              </v-btn>
            </v-row>
          </v-card-title>
          <v-card class="mx-auto mt-3">
            <v-data-table :headers="seal_doc" :items="sealWithIndex" :items-per-page="10" class="elevation-1">
              <template v-slot:item.action="{ item }">
                <v-icon color="red" @click="deleteSealFile(item)">mdi-delete</v-icon>
              </template>

              <template v-slot:item.seal_name="{ item }">
                <v-row>
                  <v-col class="align-center">
                    <a @click="openSeal(item)" class="black--text">{{ showSealname(item) }}</a>
                  </v-col>
                </v-row>
              </template>

              <template v-slot:item.seal_image="{ item }">
                <v-img class="mx-auto ma-2" contain :src="item.seal_link" width="75" height="75"/>
              </template>

              <template v-slot:item.select="{ item }">
                <v-btn text small class="success ml-6 mb-4" @click="selectedSeal(item)">
                  <v-icon>mdi-checkbox-marked-outline</v-icon>
                </v-btn>
              </template>

              <template v-slot:item.seal_status ="{ item }">
                <v-btn text small>
                  {{item.seal_status}}
                </v-btn>
              </template>

            </v-data-table>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
      <!-- Add document dialog header -->
        <v-dialog v-model="headerDialog" persistent max-width="600px">
          <v-card>
            <v-card-title
              class="headline"
            >{{ $t('company_license_register_page.tab_2.doc_dialog.title') }}</v-card-title>
            <v-card-text>
              <v-form ref="form" class="px-3 mt-8">
                <v-row dense class="align-center">
                  <v-col cols="12" xs="12" sm="12" md="12" lg="12">
                    <v-file-input
                      ref="fileUpload"
                      :label="$t('company_license_register_page.tab_2.doc_dialog.input_file')"
                      accept="image/*"
                      @change="previewImage"
                      show-size
                      filled
                    ></v-file-input>
                  </v-col>
                </v-row>
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="error"
                @click="headerDialog = !headerDialog"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.cancel_btn') }}</v-btn>
              <v-btn
                color="success"
                @click="uploadHeader"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.add_btn') }}</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <!-- Load & Save dialog -->
          <v-dialog v-model="dialog" persistent width="300">
          <v-card :color="dialog_color" dark>
            <v-card-text>
              {{ dialog_text }}
              <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
            </v-card-text>
          </v-card>
          </v-dialog>
        <!-- Snack bar -->
          <v-snackbar v-model="snack" :timeout="2000" :color="snackColor">
            {{ snackText }}
            <v-btn icon @click="snack = false"><v-icon color="white">mdi-close</v-icon></v-btn>
          </v-snackbar>
      <!-- Add document dialog header 2 -->
        <v-dialog v-model="header2Dialog" persistent max-width="600px">
          <v-card>
            <v-card-title
              class="headline"
            >{{ $t('company_license_register_page.tab_2.doc_dialog.title') }}</v-card-title>
            <v-card-text>
              <v-form ref="form" class="px-3 mt-8">
                <v-row dense class="align-center">
                  <v-col cols="12" xs="12" sm="12" md="12" lg="12">
                    <v-file-input
                      ref="fileUpload"
                      :label="$t('company_license_register_page.tab_2.doc_dialog.input_file')"
                      accept="image/*"
                      @change="previewImage"
                      show-size
                      filled
                    ></v-file-input>
                  </v-col>
                </v-row>
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="error"
                @click="header2Dialog = !header2Dialog"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.cancel_btn') }}</v-btn>
              <v-btn
                color="success"
                @click="uploadHeader2"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.add_btn') }}</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <!-- Load & Save dialog -->
          <v-dialog v-model="dialog" persistent width="300">
          <v-card :color="dialog_color" dark>
            <v-card-text>
              {{ dialog_text }}
              <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
            </v-card-text>
          </v-card>
          </v-dialog>
        <!-- Snack bar -->
          <v-snackbar v-model="snack" :timeout="2000" :color="snackColor">
            {{ snackText }}
            <v-btn icon @click="snack = false"><v-icon color="white">mdi-close</v-icon></v-btn>
          </v-snackbar>
      <!-- Add document dialog watermark -->
        <v-dialog v-model="watermarkDialog" persistent max-width="600px">
          <v-card>
            <v-card-title
              class="headline"
            >{{ $t('company_license_register_page.tab_2.doc_dialog.title') }}</v-card-title>
            <v-card-text>
              <v-form ref="form" class="px-3 mt-8">
                <v-row dense class="align-center">
                  <v-col cols="12" xs="12" sm="12" md="12" lg="12">
                    <v-file-input
                      ref="fileUpload"
                      :label="$t('company_license_register_page.tab_2.doc_dialog.input_file')"
                      accept="image/*"
                      @change="previewImage"
                      show-size
                      filled
                    ></v-file-input>
                  </v-col>
                </v-row>
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="error"
                @click="watermarkDialog = !watermarkDialog"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.cancel_btn') }}</v-btn>
              <v-btn
                color="success"
                @click="uploadWatermark"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.add_btn') }}</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <!-- Load & Save dialog -->
          <v-dialog v-model="dialog" persistent width="300">
          <v-card :color="dialog_color" dark>
            <v-card-text>
              {{ dialog_text }}
              <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
            </v-card-text>
          </v-card>
          </v-dialog>
        <!-- Snack bar -->
          <v-snackbar v-model="snack" :timeout="2000" :color="snackColor">
            {{ snackText }}
            <v-btn icon @click="snack = false"><v-icon color="white">mdi-close</v-icon></v-btn>
          </v-snackbar>
      <!-- Add document dialog seal -->
        <v-dialog v-model="sealDialog" persistent max-width="600px">
          <v-card>
            <v-card-title
              class="headline"
            >{{ $t('company_license_register_page.tab_2.doc_dialog.title') }}</v-card-title>
            <v-card-text>
              <v-form ref="form" class="px-3 mt-8">
                <v-row dense class="align-center">
                  <v-col cols="12" xs="12" sm="12" md="12" lg="12">
                    <v-file-input
                      ref="fileUpload"
                      :label="$t('company_license_register_page.tab_2.doc_dialog.input_file')"
                      accept="image/*"
                      @change="previewImage"
                      show-size
                      filled
                    ></v-file-input>
                  </v-col>
                </v-row>
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="error"
                @click="sealDialog = !sealDialog"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.cancel_btn') }}</v-btn>
              <v-btn
                color="success"
                @click="uploadSeal"
              >{{ $t('company_license_register_page.tab_2.doc_dialog.add_btn') }}</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <!-- Load & Save dialog -->
          <v-dialog v-model="dialog" persistent width="300">
          <v-card :color="dialog_color" dark>
            <v-card-text>
              {{ dialog_text }}
              <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
            </v-card-text>
          </v-card>
          </v-dialog>
        <!-- Snack bar -->
          <v-snackbar v-model="snack" :timeout="2000" :color="snackColor">
            {{ snackText }}
            <v-btn icon @click="snack = false"><v-icon color="white">mdi-close</v-icon></v-btn>
          </v-snackbar>
    </v-card>
  </v-container>
</template>

<script>
import firebase, { firestore } from "firebase"
const axios = require("axios")

export default {
  name: "Upload",
  data() {
    return {
      imageData: [null],
      uploadValue: 0,
      file_name: '',
      current: [],
      // Tab header
      tabs: '',
      // Header
      header_list: [],
      header_link: '',
      header_get_doc_id: [],
      // Header 2
      header2_list: [],
      header2_link: '',
      header2_get_doc_id: [],
      // Watermark
      watermark_list: [],
      watermark_link: '',
      watermark_get_doc_id: [],
      // Seal
      seal_list: [],
      seal_link: '',
      seal_name: '',
      seal_status: '',
      doc_seal_id:'',
      seal_get_doc_id: [],
      // Document
      headerDialog: false,
      header2Dialog: false,
      watermarkDialog: false,
      sealDialog: false,
      // Load & save dialog
      dialog: false,
      dialog_color: '',
      dialog_text: '',
      // Snack bar
      snack: false,
      snackText: '',
      snackColor: '',
      // Rule
      rules: { require: value => !!value || "required" }
    }
  },
  watch: {
    headerDialog: function() {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log("Select your file")
      }
    },
    header2Dialog: function() {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log("Select your file")
      }
    },
    watermarkDialog: function() {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log("Select your file")
      }
    },
    sealDialog: function() {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log("Select your file")
      }
    }
  },
  computed: {
    headerWithIndex() {
      return this.header_list.map((header_list, index) => ({
        ...header_list,
        index: index + 1
      }))
    },
    header2WithIndex() {
      return this.header2_list.map((header2_list, index) => ({
        ...header2_list,
        index: index + 1
      }))
    },
    watermarkWithIndex() {
      return this.watermark_list.map((watermark_list, index) => ({
        ...watermark_list,
        index: index + 1
      }))
    },
    sealWithIndex() {
      return this.seal_list.map((seal_list, index) => ({
        ...seal_list,
        index: index + 1
      }))
    },
    header_doc() {
      return [
        { text: this.$t("action"), align: "center", sortable: false, value: "action" },
        { text: this.$t("staff_logo_report.tab_1.title_1.header.no"), sortable: false, align: "center", value: "index" },
        { text: this.$t("staff_logo_report.tab_1.title_1.header.image_name"), value: "header_name" },
        { text: this.$t("staff_logo_report.tab_1.title_1.header.date_upload"), value: "header_date" },
        { text: this.$t("staff_logo_report.tab_1.title_1.header.image_preview"), sortable: false, align: 'center', value: "header_image" },
        { text: this.$t("staff_logo_report.tab_1.title_1.header.image_select"), sortable: false, align: 'center', value: "select" },
        { text: this.$t("staff_logo_report.tab_1.title_1.header.image_select"), sortable: false, align: 'center',value: "header_status" }
      ]
    },
    header2_doc() {
      return [
        { text: this.$t("action"), align: "center", sortable: false, value: "action" },
        { text: this.$t("staff_logo_report.tab_2.title_1.header.no"), sortable: false, align: "center", value: "index" },
        { text: this.$t("staff_logo_report.tab_2.title_1.header.image_name"), value: "header2_name" },
        { text: this.$t("staff_logo_report.tab_2.title_1.header.date_upload"), value: "header2_date" },
        { text: this.$t("staff_logo_report.tab_2.title_1.header.image_preview"), sortable: false, align: 'center', value: "header2_image" },
        { text: this.$t("staff_logo_report.tab_2.title_1.header.image_select"), sortable: false, align: 'center', value: "select" },
        { text: this.$t("staff_logo_report.tab_2.title_1.header.image_select"), sortable: false,align: 'center',value: "header2_status" }
      ]
    },
    watermark_doc() {
      return [
        { text: this.$t("action"), align: "center", sortable: false, value: "action" },
        { text: this.$t("staff_logo_report.tab_3.title_1.header.no"), sortable: false, align: "center", value: "index" },
        { text: this.$t("staff_logo_report.tab_3.title_1.header.image_name"), value: "watermark_name" },
        { text: this.$t("staff_logo_report.tab_3.title_1.header.date_upload"), value: "watermark_date" },
        { text: this.$t("staff_logo_report.tab_3.title_1.header.image_preview"), sortable: false, align: 'center', value: "watermark_image" },
        { text: this.$t("staff_logo_report.tab_3.title_1.header.image_select"), sortable: false, align: 'center', value: "select" },
        { text: this.$t("staff_logo_report.tab_3.title_1.header.image_select"), sortable: false,align: 'center',value: "watermark_status" }
      ]
    },
    seal_doc() {
      return [
        { text: this.$t("action"), align: "center", sortable: false, value: "action" },
        { text: this.$t("staff_logo_report.tab_4.title_1.header.no"), sortable: false, align: "center", value: "index" },
        { text: this.$t("staff_logo_report.tab_4.title_1.header.image_name"), value: "seal_name" },
        { text: this.$t("staff_logo_report.tab_4.title_1.header.date_upload"), value: "seal_date" },
        { text: this.$t("staff_logo_report.tab_4.title_1.header.image_preview"), sortable: false, align: 'center', value: "seal_image" },
        { text: this.$t("staff_logo_report.tab_4.title_1.header.image_select"), sortable: false, align: 'center', value: "select" },
        { text: this.$t("staff_logo_report.tab_4.title_1.header.image_select"), sortable: false,align: 'center',value: "seal_status" }
      ]
    }
  },
  created () {
    let localUser = localStorage.getItem('localUser')
    localUser = JSON.parse(localUser)

    try {
      if (localUser === null || localUser === undefined) {
        this.$router.replace({ name: "Login" })
      } else {
        if (localUser.type === 'admin') {
          this.dialog_text = this.$t('loading')
          this.dialog_color = 'primary'
          this.dialog = true
          this.init()
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
    async init () {
      await this.getDataSeal()
      await this.getDataHeader()
      await this.getDataHeader2()
      await this.getDataWatermark()
      this.dialog = false
    },
    // get header data
    async getDataHeader (){
      await axios.get('https://us-central1-laos-single-window.cloudfunctions.net/function/header')
      .then(res => {
        this.header_list = res.data
      })
      .catch(err => {
      console.log(err)
      })
    },
    // get header2 data
    async getDataHeader2 (){
      await axios.get('https://us-central1-laos-single-window.cloudfunctions.net/function/header2')
      .then(res => {
        this.header2_list = res.data
      })
      .catch(err => {
      console.log(err)
      })
    },
    // get watermark data
    async getDataWatermark (){
      await axios.get('https://us-central1-laos-single-window.cloudfunctions.net/function/watermark')
      .then(res => {
        this.watermark_list = res.data
      })
      .catch(err => {
      console.log(err)
      })
    },
    // get seal data
    async getDataSeal (){
      await axios.get('https://us-central1-laos-single-window.cloudfunctions.net/function/seal')
      .then(res => {
        this.seal_list = res.data
      })
      .catch(err => {
      console.log(err)
      })
    },
    // show header name
    showHeadername(item) {
      return item.header_name
    },
    // show header2 name
    showHeader2name(item) {
      return item.header2_name
    },
    // show watermark name
    showWatermarkname(item) {
      return item.watermark_name
    },
    // show seal name
    showSealname(item) {
      return item.seal_name
    },
    // preview image in table
    previewImage() {
      try {
        this.imageData = event.target.files[0]
        this.uploadValue = 0
      } catch {
        console.log("Select your file")
        this.imageData = null
      }
    },
    getTime() {
      var months_arr = ["01","02","03","04","05","06","07","08","09","10","11","12"]
      var date = new Date(Date.now())
      var year = date.getFullYear()
      var month = months_arr[date.getMonth()]
      var day = date.getDate()
      var dateTime = day + "/" + month + "/" + year

      return dateTime
    },
    // Upload Seal
    async uploadSeal() {
      let count = 0
      this.file_name = `S_${this.imageData.name}`
      for (let index = 0; index < this.seal_list.length; index++) {
        if (this.seal_list[index].seal_name === this.file_name) {
          count++
          break
        }
      }
      if (count === 0) {
        this.dialog_text = this.$t("saving")
        this.dialog_color = "success"
        this.dialog = true
        this.seal_link = null
        const storageRef = await firebase.storage().ref(this.file_name).put(this.imageData)
        await storageRef.ref.getDownloadURL().then(async url => {
          this.seal_link = url
          let data = {
            seal_id: await this.getSealCurrentID(),
            seal_name: this.file_name,
            seal_link: this.seal_link,
            seal_date: await this.getTime(),
            seal_status: 'Not Select'
          }
          this.seal_list.push(data)
          await firebase.firestore().collection("Seal_report").add(data)
          this.dialog = false
        })
        this.sealDialog = false
      } else {
        confirm(this.$t('file_duplicate')) &&
        (
          await this.resetSealInput()
        )
      }
    },
    // Reset Upload Seal
    resetSealInput () {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log('Select your file')
      }
    },
    // Upload Header
    async uploadHeader() {
      let count = 0
      this.file_name = `H_${this.imageData.name}`
      for (let index = 0; index < this.header_list.length; index++) {
        if (this.header_list[index].header_name === this.file_name) {
          count++
          break
        }
      }
      if (count === 0) {
        this.dialog_text = this.$t("saving")
        this.dialog_color = "success"
        this.dialog = true
        this.header_link = null
        const storageRef = await firebase.storage().ref(this.file_name).put(this.imageData)
        
        await storageRef.ref.getDownloadURL().then(async url => {
          this.header_link = url
          let data = {
            header_id: await this.getHeaderCurrentID(),
            header_name: this.file_name,
            header_link: this.header_link,
            header_date: await this.getTime(),
            header_status: 'Not Select'
          }
          this.header_list.push(data)
          
          await firebase.firestore().collection("Header_report").add(data)
          this.dialog = false
        })
        this.headerDialog = false
      } else {
        confirm(this.$t('file_duplicate')) &&
        (
          await this.resetHeaderInput()
        )
      }
    },
    // Reset Upload Header
    resetHeaderInput () {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log('Select your file')
      }
    },
    // Upload Header2
    async uploadHeader2() {
      let count = 0
      this.file_name = `H2_${this.imageData.name}`
      for (let index = 0; index < this.header2_list.length; index++) {
        if (this.header2_list[index].header2_name === this.file_name) {
          count++
          break
        }
      }
      if (count === 0) {
        this.dialog_text = this.$t("saving")
        this.dialog_color = "success"
        this.dialog = true
        this.header2_link = null
        const storageRef = await firebase.storage().ref(this.file_name).put(this.imageData)
        
        await storageRef.ref.getDownloadURL().then(async url => {
          this.header2_link = url
          let data = {
            header2_id: await this.getHeader2CurrentID(),
            header2_name: this.file_name,
            header2_link: this.header2_link,
            header2_date: await this.getTime(),
            header2_status: 'Not Select'
          }
          this.header2_list.push(data)
          
          await firebase.firestore().collection("Header2_report").add(data)
          this.dialog = false
        })
        this.header2Dialog = false
      } else {
        confirm(this.$t('file_duplicate')) &&
        (
          await this.resetHeader2Input()
        )
      }
    },
    // Reset Upload Header2
    resetHeader2Input () {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log('Select your file')
      }
    },
    // Upload logo Watermark
    async uploadWatermark() {
      let count = 0
      this.file_name = `H_${this.imageData.name}`
      for (let index = 0; index < this.watermark_list.length; index++) {
        if (this.watermark_list[index].watermark_name === this.file_name) {
          count++
          break
        }
      }
      if (count === 0) {
        this.file_name = `WM_${this.imageData.name}`
        this.dialog_text = this.$t("saving")
        this.dialog_color = "success"
        this.dialog = true
        this.watermark_link = null
        const storageRef = await firebase.storage().ref(this.file_name).put(this.imageData)
        
        await storageRef.ref.getDownloadURL().then(async url => {
          this.watermark_link = url
          let data = {
            watermark_id: await this.getWatermarkCurrentID(),
            watermark_name: this.file_name,
            watermark_link: this.watermark_link,
            watermark_date: await this.getTime(),
            watermark_status: 'Not Select'
          }
          this.watermark_list.push(data)
          
          await firebase.firestore().collection("Watermark_report").add(data)
          this.dialog = false
        })
        this.watermarkDialog = false
      } else {
        confirm(this.$t('file_duplicate')) &&
        (
          await this.resetWatermarkInput()
        )
      }
    },
    // Reset Upload Watermark
    resetWatermarkInput () {
      try {
        this.$refs.fileUpload.reset()
      } catch {
        console.log('Select your file')
      }
    },
    // open header for header_name
    async openHeader (item) {
      this.dialog_text = this.$t('loading')
      this.dialog_color = 'primary'
      this.dialog = true
      const fileName = item.header_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        window.open(url)
        this.dialog = false
      })
    },
    // open header2 for header2_name
    async openHeader2 (item) {
      this.dialog_text = this.$t('loading')
      this.dialog_color = 'primary'
      this.dialog = true
      const fileName = item.header2_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        window.open(url)
        this.dialog = false
      })
    },
    // open watermark for watermark_name
    async openWatermark (item) {
      this.dialog_text = this.$t('loading')
      this.dialog_color = 'primary'
      this.dialog = true
      const fileName = item.watermark_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        window.open(url)
        this.dialog = false
      })
    },
    // open seal for seal_name
    async openSeal (item) {
      this.dialog_text = this.$t('loading')
      this.dialog_color = 'primary'
      this.dialog = true
      const fileName = item.seal_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        window.open(url)
        this.dialog = false
      })
    },
    // Delete Header document in arr & DB
    async deleteHeaderFile (item) {
      confirm(this.$t('delete_item')) && 
      (
        this.dialog_text = this.$t('deleting'),
        this.dialog_color = 'error',
        this.dialog = true,

        await firebase.storage().ref(item.header_name).delete()
        .then(async url => {
          await this.deleteHeader(item.header_id)
          const index = Number(item.index) - 1
          this.header_list.splice(index, 1),
          this.snack = true,
          this.snackText = this.$t("company_license_register_page.snackbar_del"),
          this.snackColor = 'error',
          this.dialog = false
        })
        .catch(err => {
          console.log(err)
        })
      )
    },
    // Delete Header document in DB
    async deleteHeader (doc_id) {
      await firebase.firestore().collection('Header_report').where('header_id', '==', Number(doc_id)).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Header_report').doc(docs.id).delete()
        })
      })
    },
    // Delete Header2 document in arr & DB
    async deleteHeader2File (item) {
      confirm(this.$t('delete_item')) && 
      (
        this.dialog_text = this.$t('deleting'),
        this.dialog_color = 'error',
        this.dialog = true,

        await firebase.storage().ref(item.header2_name).delete()
        .then(async url => {
          await this.deleteHeader2(item.header2_id)
          const index = Number(item.index) - 1
          this.header2_list.splice(index, 1),
          this.snack = true,
          this.snackText = this.$t("company_license_register_page.snackbar_del"),
          this.snackColor = 'error',
          this.dialog = false
        })
        .catch(err => {
          console.log(err)
        })
      )
    },
    // Delete Header2 document in DB
    async deleteHeader2 (doc_id) {
      await firebase.firestore().collection('Header2_report').where('header2_id', '==', Number(doc_id)).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Header2_report').doc(docs.id).delete()
        })
      })
    },
    // Delete Watermark document in arr & DB
    async deleteWatermarkFile (item) {
      confirm(this.$t('delete_item')) && 
      (
        this.dialog_text = this.$t('deleting'),
        this.dialog_color = 'error',
        this.dialog = true,

        await firebase.storage().ref(item.watermark_name).delete()
        .then(async url => {
          await this.deleteWatermark(item.watermark_id)
          const index = Number(item.index) - 1
          this.watermark_list.splice(index, 1),
          this.snack = true,
          this.snackText = this.$t("company_license_register_page.snackbar_del"),
          this.snackColor = 'error',
          this.dialog = false
        })
        .catch(err => {
          console.log(err)
        })
      )
    },
    // Delete Watermark document in DB
    async deleteWatermark (doc_id) {
      await firebase.firestore().collection('Watermark_report').where('watermark_id', '==', Number(doc_id)).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Watermark_report').doc(docs.id).delete()
        })
      })
    },
    // Delete Seal document in arr & DB
    async deleteSealFile (item) {
      confirm(this.$t('delete_item')) && 
      (
        this.dialog_text = this.$t('deleting'),
        this.dialog_color = 'error',
        this.dialog = true,

        await firebase.storage().ref(item.seal_name).delete()
        .then(async url => {
          await this.deleteSeal(item.seal_id)
          const index = Number(item.index) - 1
          this.seal_list.splice(index, 1),
          this.snack = true,
          this.snackText = this.$t("company_license_register_page.snackbar_del"),
          this.snackColor = 'error',
          this.dialog = false
        })
        .catch(err => {
          console.log(err)
        })
      )
    },
    // Delete Seal document in DB
    async deleteSeal (doc_id) {
      await firebase.firestore().collection('Seal_report').where('seal_id', '==', Number(doc_id)).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Seal_report').doc(docs.id).delete()
        })
      })
    },
    // Get Current_ID for update header_id
    async getHeaderCurrentID () {
      let data = await firebase.firestore().collection('Current_ID').doc('doc_1').get()
      await this.updateCurrentHeaderID()
      return  data.data().header_id
    },
    // Get update header_id
    async updateCurrentHeaderID () {
      await firebase.firestore().collection('Current_ID').doc('doc_1').update({
        header_id: firebase.firestore.FieldValue.increment(1)
      })
    },
    // Get Current_ID for update header2_id
    async getHeader2CurrentID () {
      let data = await firebase.firestore().collection('Current_ID').doc('doc_1').get()
      await this.updateCurrentHeader2ID()
      return  data.data().header2_id
    },
    // Get update header2_id
    async updateCurrentHeader2ID () {
      await firebase.firestore().collection('Current_ID').doc('doc_1').update({
        header2_id: firebase.firestore.FieldValue.increment(1)
      })
    },
    // Get Current_ID for update watermark_id
    async getWatermarkCurrentID () {
      let data = await firebase.firestore().collection('Current_ID').doc('doc_1').get()
      await this.updateCurrentWatermarkID()
      return  data.data().watermark_id
    },
    // Get update watermark_id
    async updateCurrentWatermarkID () {
      await firebase.firestore().collection('Current_ID').doc('doc_1').update({
        watermark_id: firebase.firestore.FieldValue.increment(1)
      })
    },
    // Get Current_ID for update seal_id
    async getSealCurrentID () {
      let data = await firebase.firestore().collection('Current_ID').doc('doc_1').get()
      await this.updateCurrentSealID()
      return data.data().seal_id
    },
    // Get update seal_id
    async updateCurrentSealID () {
      await firebase.firestore().collection('Current_ID').doc('doc_1').update({
        seal_id: firebase.firestore.FieldValue.increment(1)
      })
    },
    // Select Header from table
    async selectedHeader(item){
      this.dialog_text = this.$t("saving")
      this.dialog_color = "success"
      this.dialog = true
      
      let check_header = item.header_name
      let doc_header_id = item.header_id

      await firebase.firestore().collection('Current_Seal').doc('seal_1').update({
        header_name: check_header
      })

      await this.changeHeaderStatusSelected(doc_header_id)  
      this.dialog = false
      this.HeaderDialog = false
    },
    // Update Status Select
    async changeHeaderStatusSelected (doc_header_id){
      // Get document id from Header_report
      await firebase.firestore().collection('Header_report').get()
      .then(snapshot => {
        snapshot.forEach(doc => {
          this.header_get_doc_id.push(doc.id)
        })
      })
      // Update All Status is "Not Select"
      for(let i=0;i<this.header_get_doc_id.length;i++){
        await firebase.firestore().collection('Header_report').doc(this.header_get_doc_id[i]).update({
          header_status: 'Not Select'
        })
      }
      // Update Status is "Selected"
      await firebase.firestore().collection('Header_report').where('header_id', '==', doc_header_id).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Header_report').doc(docs.id).update({
            header_status: 'Selected'
          })
          await this.getDataHeader()
        })
      })
    },
    // Select Header2 from table
    async selectedHeader2(item){
      this.dialog_text = this.$t("saving")
      this.dialog_color = "success"
      this.dialog = true
      
      let check_header2 = item.header2_name
      let doc_header2_id = item.header2_id

      await firebase.firestore().collection('Current_Seal').doc('seal_1').update({
        header2_name: check_header2
      })

      await this.changeHeader2StatusSelected(doc_header2_id)  
      this.dialog = false
      this.Header2Dialog = false
    },
    // Update Status Select
    async changeHeader2StatusSelected (doc_header2_id){
      // Get document id from Header_report
      await firebase.firestore().collection('Header2_report').get()
      .then(snapshot => {
        snapshot.forEach(doc => {
          this.header2_get_doc_id.push(doc.id)
        })
      })
      // Update All Status is "Not Select"
      for(let i=0;i<this.header2_get_doc_id.length;i++){
        await firebase.firestore().collection('Header2_report').doc(this.header2_get_doc_id[i]).update({
          header2_status: 'Not Select'
        })
      }
      // Update Status is "Selected"
      await firebase.firestore().collection('Header2_report').where('header2_id', '==', doc_header2_id).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Header2_report').doc(docs.id).update({
            header2_status: 'Selected'
          })
          await this.getDataHeader2()
        })
      })
    },
    // Select Watermark from table
    async selectedWatermark(item){
      this.dialog_text = this.$t("saving")
      this.dialog_color = "success"
      this.dialog = true
      
      let check_watermark = item.watermark_name
      let doc_watermark_id = item.watermark_id

      await firebase.firestore().collection('Current_Seal').doc('seal_1').update({
        watermark_name: check_watermark
      })

      await this.changeWatermarkStatusSelected(doc_watermark_id)  
      this.dialog = false
      this.WatermarkDialog = false
    },
    // Update Status Select
    async changeWatermarkStatusSelected (doc_watermark_id){
      // Get document id from Header_report
      await firebase.firestore().collection('Watermark_report').get()
      .then(snapshot => {
        snapshot.forEach(doc => {
          this.watermark_get_doc_id.push(doc.id)
        })
      })
      // Update All Status is "Not Select"
      for(let i=0;i<this.watermark_get_doc_id.length;i++){
        await firebase.firestore().collection('Watermark_report').doc(this.watermark_get_doc_id[i]).update({
          watermark_status: 'Not Select'
        })
      }
      // Update Status is "Selected"
      await firebase.firestore().collection('Watermark_report').where('watermark_id', '==', doc_watermark_id).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Watermark_report').doc(docs.id).update({
            watermark_status: 'Selected'
          })
          await this.getDataWatermark()
        })
      })
    },
    // Select Seal from table
    async selectedSeal(item){
      this.dialog_text = this.$t("saving")
      this.dialog_color = "success"
      this.dialog = true
      
      let check_seal = item.seal_name
      let doc_seal_id = item.seal_id

      await firebase.firestore().collection('Current_Seal').doc('seal_1').update({
        seal_name: check_seal
      })

      await this.changeSealStatusSelected(doc_seal_id)
      this.dialog = false
      this.sealDialog = false
    },
    // Update Status Select
    async changeSealStatusSelected (doc_seal_id){
      // Get document id from Seal_report
      await firebase.firestore().collection('Seal_report').get()
      .then(snapshot => {
        snapshot.forEach(doc => {
          this.seal_get_doc_id.push(doc.id)
        })
      })
      // Update All Status is "Not Select"
      for(let i=0;i<this.seal_get_doc_id.length;i++){
        await firebase.firestore().collection('Seal_report').doc(this.seal_get_doc_id[i]).update({
          seal_status: 'Not Select'
        })
      }
      // Update Status is "Selected"
      await firebase.firestore().collection('Seal_report').where('seal_id', '==', doc_seal_id).get()
      .then(snapshot => {
        snapshot.forEach(async docs => {
          await firebase.firestore().collection('Seal_report').doc(docs.id).update({
            seal_status: 'Selected'
          })
          await this.getDataSeal()
        })
      })
    }
  }
}
</script>
