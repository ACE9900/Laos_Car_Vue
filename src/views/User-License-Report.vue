<template>
  <v-container>
    <!-- logo Watermarker -->
    <v-row align="center" justify="center">
      <v-img class="watermark_style mt-12" contain :src="this.watermark_image"></v-img>
    </v-row>
    <!-- logo Header -->
      <v-row align="center" justify="center" class="mt-2">
        <v-img class="header_style mx-12 mt-2" contain max-width="80" max-height="80" :src="this.header_image"/>
      </v-row>
    <!-- logo Header2 -->
        <v-img class="header2_style mx-2 mt-2" contain max-width="110" max-height="110" :src="this.header2_image"/>
          
<!-- Lao People's Democratic Republic -->
      <v-row align="center" justify="center" class="mt-4">
      </v-row>
        <div class="text-center justify-center mb-6 mt-12">
          <h3 class="font-weight-bold">ສາທາລະນະລັດ ປະຊາທິປະໄຕ ປະຊາຊົນລາວ</h3>
          <h3 class="font-weight-bold">ສັນຕິພາບ ເອກະລາດ ປະຊາທິປະໄຕ ເອກະພາບ ວັດທະນະຖາວອນ</h3>
          <h3 class="font-weight-bold">LAO PEOPLE'S DEMOCRATIC REPUBILC</h3>
          <h3 class="font-weight-bold">PEACE INDEPEDENCE DEMOCRACY UNITY PROSPERITY</h3>
        </div>
<!-- Ministry of Public Work and Transport -->
      <div class="text-left">
          <h2 class="ml-2">ກະຊວງໂຍທາທິການແລະຂົນສົ່ງ / Ministry of Public Work and Transport</h2>
          <v-row class="ml-2">
            <h2 class="">ກົມຂົນສົ່ງ / Department of Transport</h2>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-10"></h1>
              <h2 class=" ml-8">ເລກທີ / Reference No:</h2>
              <h2 class=" ml-10">{{data_report.app_approve_id}}</h2>
              <h1 class="subtitle-2 ml-10"></h1>
            <h2 class=" ml-3">ກຂສ / DOT </h2>
          </v-row>
      </div>

      <div class="text-left">
        <v-row class="ml-12">
            <h1 class="subtitle-2 ml-12"></h1>
            <h1 class="subtitle-2 ml-12"></h1>
            <h1 class="subtitle-2 ml-12"></h1>
            <h1 class="subtitle-2 ml-12"></h1>
            <h1 class="subtitle-2 ml-6"></h1>
          <h2 class="ml-8">ນະຄອນຫຼວງວຽງຈັນ / Vientiane</h2>
          <h2 class="ml-4">ວັນທີ / Date:</h2>
          <h2 class="ml-10">{{data_report.app_date_req}}</h2>
        </v-row>
      </div>
<!-- Vehicle Technical Import License -->
      <div class="text-center justify-center mt-1">
        <h3 class="font-weight-bold">ໃບອະນຸຍາດນຳເຂົ້າທາງດ້ານເຕັກນິກຍານພາຫະນະ / Vehicle Technical Import License</h3>
      </div>

      <div class="text-left justify-left mt-1">
        <v-row class="ml-2">
          <h1>- ອິງຕາມກົດໝາຍວ່າດ້ວຍການຈາລະຈອນທາງບົກ ເລກທີ 23/ສພຊ,ລົງວັນທີ 12/12/2012 / Reference to Land Traffic Law, Issued No:23/NA</h1><h1 class="ml-4">Date : 12 Dec 2012</h1>
          <!-- <h1 class=" ml-4">Date : 12 Dec 2012</h1> -->
          </v-row>
          <v-row class="ml-2">
            <h1>- ອິງຕາມໃບອະນຸຍາດນຳເຂົ້າເລກທີ / Reference to Import License No: {{data_report.app_import_license_no}}</h1>
            <h1 class=" ml-12">ກຂອ / DIMEX,</h1><h1 class=" ml-4"> ວັນທີ / Date: {{data_report.app_import_license_date}}</h1>
          </v-row>
          
      </div>
<!-- The Department of Transport grants the import Vehicle Technical Approval to : -->
      <div class="text-center justify-left">
          <h4 class="font-weight-bold mt-4">ກົມຂົນສົ່ງເຫັນດີອອກອະນຸຍາດນຳເຂົ້າທາງດ້ານເຕັກນິກນຳຍານພາຫະນະໃຫ້ແກ່ / The Department of Transport grants the import Vehicle Technical Approval to : </h4>
          <v-row  class="ml-4">
              <h1 class="">{{data_comp.comp_name}}</h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class="subtitle-2 ml-12"></h1>
              <h1 class=" ml-12">ໂທລະສັບ / Telephone : {{data_comp.comp_tel}}</h1>
              <h1 class=" ml-12">ແຟັກ / Fax : {{data_comp.comp_fax}}</h1>
          </v-row>
      </div>
      
<!-- Purpose of Import / Specifications / Vehicle Identity / Remark -->
  <!-- Purpose of Import -->
        <v-row class="ml-2 my-1">
          <h2 class="font-weight-bold">1.</h2>
              <h1 class="subtitle-2 ml-8"></h1>
          <h2 class="font-weight-bold">ຈຸດປະສົງໃນການນຳເຂົ້າ / Purpose of Import :</h2>
          <h2 class="font-weight-bold ml-8">{{data_report.app_purpose}}</h2>
        </v-row>
  <!-- Specifications -->
        <v-row class="ml-2 my-1">
          <h2 class="font-weight-bold">2.</h2>
              <h1 class="subtitle-2 ml-8"></h1>
          <h2 class="font-weight-bold">ຂໍ້ມູນທົ່ວໄປທາງດ້ານເຕັກນິກ / Specifications</h2>
        </v-row>
    <!-- Specifications Table -->
        <v-simple-table dense class="mx-3 transparent" id="spec">
          <template v-slot:default>
            <thead>
            <!-- Table Row #1 -->
              <tr>
                <td><h1 class="text-left">ປະເພດລົດ / Classification: {{data_table.item_car_type}}</h1></td>
                <td><h1 class="text-left">ປີຜະລິດ / Model Year: {{data_table.item_car_manufacture}}</h1></td>
                <td><h1 class="text-left">ພວງມະໄລ / Steering: {{data_table.item_car_steering}}</h1></td>
                <td><h1 class="text-left">ຈຳນວນບ່ອນນັ່ງ / Seat: {{data_table.item_car_seat}}</h1></td>
              </tr>
            <!-- Table Row #2 -->
              <tr>
                <td><h1 class="text-left">ຍີ່ຫໍ້ / Maker: {{data_table.item_car_brand}}</h1></td>
                <td><h1 class="text-left">ຈຳນວນລໍ້ / Wheel: {{data_table.item_car_wheels}}</h1></td>
                <td><h1 class="text-left">ຈຳນວນເພົາ / Axle: {{data_table.item_car_axels}}</h1></td>
                <td rowspan="2"><v-row align="center"><h1 class="text-left">ສະພາຍເຕັກນິກ / Technical Conditions: </h1></v-row>
                  <v-row>
                      <v-checkbox v-model="checkbox1" color="black" label="80%" class="text-left ml-2 my-0" readonly dense hide-details></v-checkbox>
                      <v-checkbox v-model="checkbox2" color="black" label="100%" class="text-left ml-2 my-0" readonly dense hide-details ></v-checkbox>
                  </v-row>
                </td>
              </tr>
            <!-- Table Row #3 -->
              <tr>
                <td><h1 class="text-left">ລຸ້ນ / Model: {{data_table.item_car_gen}}</h1></td>
                <td colspan="2"><h1 class="text-left">ນຳໃຊ້ພະລັງງານ / Energy: {{data_table.item_car_gas}}</h1></td>
              </tr>
            <!-- Table Row #4 -->
              <tr>
                <td><h1 class="text-lef font-weight ">ຄວາມແຮງ / Displacement: {{data_format.car_power}}CC</h1></td>
                <td colspan="3">
                  <v-row>
                    <h1 class="text-left ml-3">ນ້ຳໜັກລວມ / Gross: {{data_format.car_total_weight}} (kg.)</h1>
                    <h1 class="text-left ml-12"></h1>
                    <h1 class="text-left ml-12"></h1>
                    <h1 class="text-left ml-12">ນ້ຳໜັກເປົ່າ / Curb : {{data_format.car_weight}} (kg.)</h1>
                  </v-row>
                </td>
              </tr>
            <!-- Table Row #5 -->
              <tr>
                <td colspan="4">
                  <v-row>
                    <h1 class="text-left ml-3">ຂະໜາດລົດ / Dimensions:</h1>
                    <h1 class="text-left ml-3">ຄວາມສູງ / Height: {{data_format.car_height}} (mm.)</h1>
                    <h1 class="text-left ml-12">ຄວາມຍາວ / Length: {{data_format.car_long}} (mm.)</h1>
                    <h1 class="text-left ml-12">ຄວາມກວ້າງ / Width: {{data_format.car_wide}} (mm.)</h1>
                  </v-row>
                </td>
              </tr>
              <tr>
              </tr>
            </thead>
          </template>
        </v-simple-table>
  <!-- Vehicle Identity -->        
        <v-row class="ml-2 my-1">
          <h2 class="font-weight-bold">3.</h2>
              <h1 class="subtitle-2 ml-8"></h1>
          <h2 class="font-weight-bold">ຂໍ້ມູນສະເພາະຂອງຍານພະຫະນະ / Vehicle Identity</h2>
        </v-row>
    <!-- Table #2 -->
        <v-simple-table dense class="mx-5 transparent" color="black" id="vehicle">
          <template v-slot:default>
            <thead>
              <tr>
                <td class="text-center font-weight-bold td--text">ລ/ດ / No</td>
                <td class="text-center font-weight-bold td--text">ເລກຈັກ / Engine Number</td>
                <td class="text-center font-weight-bold td--text">ເລກຖັງ / Chassis Number</td>
                <td class="text-center font-weight-bold td--text">ສີ /Color</td>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in data_number" :key="item.no">
                <td class="text-center font-weight td--text">{{ item.no }}</td>
                <td class="text-center font-weight td--text">{{ item.engine_number }}</td>
                <td class="text-center font-weight td--text">{{ item.tank_number }}</td>
                <td class="text-center font-weight td--text">{{ item.color }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
  <!-- Remark -->
        <v-row class="ml-2 my-1">
          <h2 class="font-weight-bold">4.</h2>
              <h1 class="subtitle-2 ml-8"></h1>
          <h2 class="font-weight-bold">ໝາຍເຫດ / Remark</h2>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="subtitle-2 ml-8"></h1>
          <h1 class="font-weight">ຫົວໜ້າກົມ / director general</h1>
        </v-row>

        <v-row align="center" class="my-0">
          <div class="text-center ml-6">
            <v-row class="ml-5 mt-1">
              <h1 class="font-weight-bold">1)</h1>
                  <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="font-weight">ຍານພາຫະນະທີ່ໄດ້ຮັບອະນຸຍາດຕ້ອງນຳເຂົ້າກ່ອນວັນທີ / The Vehicles must be imported before : {{data_report.app_date_expire}}</h1>
            </v-row>
            <v-row class="ml-5">
              <h1 class="font-weight-bold">2)</h1>
                  <h1 class="subtitle-2 ml-8"></h1>
              <h1 class="font-weight">ດ່ານນຳເຂົ້າ / Custom Clearance Office : {{data_report.app_clearance_office}}</h1>
            </v-row>
          </div>
        <div class="mx-12">
<!-- logo Seal -->
          <v-img class="seal_style ml-6" contain max-width="100" max-height="100" :src="this.seal_image" />
        </div>  
    </v-row>
    <div>
        <v-btn class="print" id="printPageButton" color="primary" @click="onPrint">Print</v-btn>
    </div>
    <v-dialog v-model="loadDialog" persistent width="300">
      <v-card color="primary" dark>
        <v-card-text>
          {{ $t('loading') }}
          <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
        </v-card-text>
      </v-card> 
    </v-dialog>

  </v-container>
</template>

<script>
import firebase from "firebase"

export default {
  data (){
    return{
      loadDialog: false,
      // Checkbox data
      checkbox1: null,
      checkbox2: null,
      // Report data
      data_table:{},
      data_report:{},
      data_comp:{},
      data_format:{},
      data_number:[],
      // data_str:{},
      data_image:{},
      seal_image: '',
      header_image: '',
      header2_image: '',
      watermark_image: ''
    }
  },
  async mounted() {
    this.loadDialog = true
    await this.table_Specifications()
    await this.getCurrentSeal()
  },
  methods: {
    onPrint (){
      window.print()
    },
    // Show checkbox
    onCheck (){
      let data_check = this.data_table.item_standard
      if(data_check == "80 %"){
        this.checkbox1 = true
      }else if(data_check == "100 %"){
        this.checkbox2 = true
      }
    },
    // Show data
    async table_Specifications() {
      let get_id = Number(this.$route.params.id)
      const db = firebase.firestore()
      // Get data from Item_detail
      this.data_table = await db.collection("Item_detail").where("app_id","==",get_id).get()
      .then(snapshot => {
        let data = {}
          snapshot.forEach(doc => {
            data = doc.data()
          })
          return data
      })
      await this.onCheck(this.data_table)
      await this.setFormat(this.data_table)
      await this.table_Vehicle_Identity(this.data_table)

      // Get data from Application_form
      this.data_report = await db.collection("Application_form").where("app_id","==",get_id).get()
      .then(snapshot => {
        let data = {}
          snapshot.forEach(doc => {
            data = doc.data()
          })
          return data
      })
      await this.showData()
      
    // Get data from Application_form_detail
    // this.data_str = await db.collection("Application_form_detail").where("app_detail_id","==",this.data_report.app_detail_id).get()
    //   .then(snapshot => {
    //     let data = {}
    //       snapshot.forEach(doc => {
    //       data = doc.data()
    //     })
    //     return data
    // })
      // this.loadDialog = false
    },
    // Get data from Company 
    async showData (){
      let comp_data = Number(this.data_report.comp_id)
      const db = firebase.firestore()
      this.data_comp = await db.collection("Company").where("comp_id","==",comp_data).get()
        .then(snapshot => {
          let data = {}
            snapshot.forEach(doc => {
            data = doc.data()
          })
          return data
      })
    },
    // Set format data
    setFormat (){
      this.data_format = {
          car_power: this.getNumFormat(this.data_table.item_car_power), 
          car_weight: this.getNumFormat(this.data_table.item_car_weight) , 
          car_total_weight: this.getNumFormat(this.data_table.item_car_total_weight), 
          car_height: this.getNumFormat(this.data_table.item_car_height), 
          car_long: this.getNumFormat(this.data_table.item_car_long), 
          car_wide: this.getNumFormat(this.data_table.item_car_wide)
      }
    },
    // Format data
    getNumFormat (value, decimal) {
      const format = Number(parseFloat(Number(value)).toFixed(2)).toLocaleString('en', {
        minimumFractionDigits: decimal
      })
      return format
    },
    // Get data tank engine and color from item_car_tech 
    table_Vehicle_Identity(){
      let count = this.data_table.item_car_tech.length - 1
      for(let i=0;i<this.data_table.item_car_tech.length;i++){
          this.data_number.push({
          no: i+1, 
          tank_number: this.data_table.item_car_tech[i].tank_number, 
          engine_number: this.data_table.item_car_tech[i].engine_number, 
          color: this.data_table.item_car_tech[i].color
        })
        if(count===i){
          for(let j=count+1;j<20;j++){
            this.data_number.push({no: j+1, tank_number: null, engine_number: null, color: null})
          }
        }
      }
    },
    // Get seal_name from Current_Seal
    async getCurrentSeal () {
      const db = firebase.firestore()
      this.data_image = await db.collection("Current_Seal").get()
        .then(snapshot => {
          let data = {}
            snapshot.forEach(doc => {
            data = doc.data()
          })
          return data
      })
      await this.previewSeal()
      await this.previewHeader()
      await this.previewHeader2()
      await this.previewWatermark()
      this.loadDialog = false
    },
    // Preview Seal for Report
    async previewSeal (data_image) {
      const fileName = this.data_image.seal_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        this.seal_image = url
        // this.bg_img = url
      })
    },
    // Preview Header for Report
    async previewHeader (data_image) {
      const fileName = this.data_image.header_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        this.header_image = url
      })
    },
    // Preview Header2 for Report
    async previewHeader2 (data_image) {
      const fileName = this.data_image.header2_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        this.header2_image = url
      })
    },
    // Preview Watermark for Report
    async previewWatermark (data_image) {
      const fileName = this.data_image.watermark_name

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        this.watermark_image = url
      })
    }
  }
}
</script>

<style scoped>
/* Watermarker Style */
.watermark_style {
  width: 400px;
  height: 400px;
  position: absolute;
  top: 30%;
  left: 50%;
  margin-top: -200px;
  margin-left: -200px;
  background-repeat: no-repeat;
  background-size: 50%;
  opacity:0.2;
}
/* Header Style */
.header_style {
  width: 400px;
  height: 400px;
  position: absolute;
  top: 0%;
  left: 40%;
  margin-top: -200px;
  margin-left: -200px;
}
/* Header2 Style */
.header2_style {
  width: 400px;
  height: 400px;
  position: absolute;
  top: 9%;
  left: 5%;
  margin-top: -200px;
  margin-left: -200px;
  background-repeat: no-repeat;
}
/* Seal Style */
.seal_style {
  width: 400px;
  height: 400px;
  position: absolute;
  top: 101%;
  left: 69%;
  margin-top: -200px;
  margin-left: -200px;
  background-repeat: no-repeat;
}
/* Spec table Style */
#spec td, #spec th {
  border: 0.25px solid black;
}
#spec h1 {
  font-size: 10px;
}
/* Vehicle table Style */
#vehicle td, #vehicle th {
  border: 0.25px solid black;
  height: 1px;
  color: black;
  font-size: 10px !important;
  font-family: phet;
}
#vehicle v-simple-table {
  width: 100%;
}
/* Text Style */
h1 {
  font-size: 10px;
  font-family: phet;
}
/* Text Purpose and Other */
h2 {
  font-size: 12px;
  font-family: phet;
}
/* Text Header */
h3 {
  font-size: 15px;
  font-family: phet;
}
/* The Department of Transport */
h4 {
  font-size: 11px;
  font-family: phet;
}
/* Print Style */
@media print {
  #printPageButton {
    display: none;  
  }
}
/* Fonts Laos Style */
@font-face {
  src: url(fonts/Phetsarath-Regular.ttf);
  font-family: phet;
}
/* Page Style */
@page {
   margin: 4mm;
}
</style scoped>