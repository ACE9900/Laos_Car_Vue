<template>
    <nav>
        <v-app-bar 
          app
          class="yellow lighten-1"
          flat
          :prominent="prominent"
          v-model="appbar"
        >
        <v-btn
          class="mr-5"
          v-if="drawerButton"
          icon
          @click="drawer = !drawer"
        >
          <v-icon>mdi-view-list</v-icon>
        </v-btn>
        <!-- Show logo big size and project name at Login, Register and Wait Result -->
        <v-row class="my-auto" v-if="checkPage">
          <v-col cols="12" xs="12" sm="12" md="1" lg="1">
            <v-avatar size="100">
                <img
                  src="../assets/laos logo.png" 
                  alt="logo"
                >
            </v-avatar>
          </v-col>
          <v-col cols="12" xs="12" sm="12" md="11" lg="11" class="font-italic font-weight-bold px-1 mt-2">
            <h2>Vehicle Technical Import License</h2>
            <h2 class="body-2 ml-2">by Lao People's Democratic Republic</h2>
          </v-col>
        </v-row>
        <!-- Show logo small size and project name at Main Program -->
        <v-row class="my-auto" v-else>
          <h3 class="font-italic font-weight-bold">
            <v-avatar size="50">
              <img
                src="../assets/laos logo.png"
                alt="logo"
              >
            </v-avatar>Vehicle Technical Import License
          </h3>
        </v-row>
          <!-- Instruction -->
          <v-tooltip bottom>
            <template v-slot:activator="{ on }">
              <v-btn text v-on="on" @click="openFile">
                <v-icon color="primary">
                  mdi-help-circle
                </v-icon>
              </v-btn>
            </template>
            <span>{{ $t('navbar.instruction') }}</span>
          </v-tooltip>|
          <!-- Select language -->
          <v-menu select origin="center center" transition="scale-transition" inline absolute>
            <template v-slot:activator="{ on }">
              <v-btn text v-on="on">
                <country-flag class="mr-1" :country="$t('flag')"/>
                {{ $t('flag') }}
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                v-for="(lang, index) in languages"
                :key="index"
                @click="changeLanguage(lang)"
              >
              <v-list-item-icon>
                <country-flag :country='lang.value'/>
              </v-list-item-icon>
              <v-list-item-title>{{ lang.title }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
          <!-- Show user login -->
          <div v-if="isLogin" class="mr-3">
            <v-row v-if="loggedIn" class="align-center">
              <v-icon class="mx-2">mdi-account-circle</v-icon>
              <h5> :  {{ user }}</h5>
            </v-row>
          </div>
        </v-app-bar>
        <!-- Show Navigation Drawer -->
        <v-navigation-drawer 
          app
          v-model="drawer"
          floating
          mobile-break-point="991"
          width="265"
          class="grey darken-3"
        >
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title>
                <v-row class="justify-center align-center" style="height: 40px">
                  <h2 class="white--text">{{ $t('navbar.menu') }}</h2>
                </v-row>
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider class="white mx-3" />
          <!-- Show if admin -->
          <div v-if="isAdmin">
            <v-list-group
              v-for="header in admin"
              :key="header.title"
              class="my-1 px-2"
              color="white"
              :value="header.index"
            >
              <template v-slot:activator>
                <v-icon color="white" class="mr-2">{{ header.icon }}</v-icon>
                <v-list-item-title class="white--text">{{ header.title }}</v-list-item-title>
              </template>
              <div v-if="header.index">
                <v-list-item
                  to="/staff_register_list"
                  color="white"
                  active-class="amber darken-1"
                  class="my-2"
                  dark
                >
                  <v-list-item-title class="white--text" v-text="$t('navbar.register_list')"></v-list-item-title>
                  <v-list-item-icon>
                    <v-icon color="white">mdi-clipboard-list</v-icon>
                  </v-list-item-icon>
                </v-list-item>

                <v-list-item
                  v-if="$route.name === 'Staff-Register-Approve'"
                  to="/staff_register_approve/"
                  color="white"
                  active-class="amber darken-1"
                  class="my-2"
                  disabled
                  dark
                >
                  <v-list-item-title class="white--text" v-text="$t('navbar.register_detail')"></v-list-item-title>
                  
                  <v-list-item-icon>
                    <v-icon color="white">mdi-account-details</v-icon>
                  </v-list-item-icon>
                </v-list-item>
              </div>

              <div v-else>
                <v-list-item
                  to="/staff_license_list"
                  color="white"
                  active-class="amber darken-1"
                  class="my-2"
                  dark
                >
                  <v-list-item-title class="white--text" v-text="$t('navbar.license_list')"></v-list-item-title>
                  <v-list-item-icon>
                    <v-icon color="white">mdi-clipboard-list</v-icon>
                  </v-list-item-icon>
                </v-list-item>

                <v-list-item
                  v-if="$route.name === 'Staff-License-Approve'"
                  to="/staff-license-approve/"
                  color="white"
                  active-class="amber darken-1"
                  class="my-2"
                  disabled
                  dark
                >
                  <v-list-item-title class="white--text" v-text="$t('navbar.license_detail')"></v-list-item-title>
                  
                  <v-list-item-icon>
                    <v-icon>mdi-file-edit</v-icon>
                  </v-list-item-icon>
                </v-list-item>
              </div>
            </v-list-group>
            <v-list-item
              v-for="item in logo_report"
              :key="item.title"
              :to="item.link"
              color="white"
              active-class="amber darken-1"
              class="mx-2"
              dark
            >
              <v-list-item-icon>
                <v-icon color="white">{{ item.icon }}</v-icon>
              </v-list-item-icon>

              <v-list-item-title class="white--text" v-text="item.title"></v-list-item-title>
            </v-list-item>
          </div>
          <!-- Show if staff -->
          <div v-if="isStaff">
            <v-list-group
              v-for="header in staff"
              :key="header.title"
              class="my-1 px-2"
              color="white"
              :value="header.index"
            >
              <template v-slot:activator>
                <v-icon color="white" class="mr-2">{{ header.icon }}</v-icon>
                <v-list-item-title class="white--text">{{ header.title }}</v-list-item-title>
              </template>
                <v-list-item
                  to="/staff_license_list"
                  color="white"
                  active-class="amber darken-1"
                  class="my-2"
                  dark
                >
                  <v-list-item-title class="white--text" v-text="$t('navbar.license_list')"></v-list-item-title>
                  <v-list-item-icon>
                    <v-icon color="white">mdi-clipboard-list</v-icon>
                  </v-list-item-icon>
                </v-list-item>

                <v-list-item
                  v-if="$route.name === 'Staff-License-Approve'"
                  to="/staff-license-approve/"
                  color="white"
                  active-class="amber darken-1"
                  class="my-2"
                  disabled
                  dark
                >
                  <v-list-item-title class="white--text" v-text="$t('navbar.license_detail')"></v-list-item-title>
                  
                  <v-list-item-icon>
                    <v-icon>mdi-file-edit</v-icon>
                  </v-list-item-icon>
                </v-list-item>
            </v-list-group>
          </div>
          <!-- Show if company -->
          <div v-if="isCompany">
            <v-list-group
              v-for="header in company"
              :key="header.title"
              class="my-1 px-2"
              color="white"
              :value="header.index"
            >
              <template v-slot:activator>
                <v-icon color="white" class="mr-2">{{ header.icon }}</v-icon>
                <v-list-item-title class="white--text">{{ header.title }}</v-list-item-title>
              </template>

              <v-list-item
                to="/user_license_list"
                color="white"
                active-class="amber darken-1"
                class="my-2"
                dark
              >
                <v-list-item-title v-text="$t('navbar.license_list')"></v-list-item-title>

                <v-list-item-icon>
                  <v-icon>mdi-clipboard-list</v-icon>
                </v-list-item-icon>
              </v-list-item>

               <v-list-item
                v-if="$route.name === 'User-License-Detail'"
                to="/license_detail/"
                color="white"
                active-class="amber darken-1"
                class="my-2"
                disabled
                dark
              >
                <v-list-item-title v-text="$t('navbar.license_detail')"></v-list-item-title>

                <v-list-item-icon>
                  <v-icon>mdi-file-edit</v-icon>
                </v-list-item-icon>
              </v-list-item>

              <v-list-item
                v-if="$route.name === 'User-License-Register'"
                to="/license_register"
                color="white"
                active-class="amber darken-1"
                class="my-2"
                disabled
                dark
              >
                <v-list-item-title v-text="$t('navbar.license_register')"></v-list-item-title>

                <v-list-item-icon>
                  <v-icon>mdi-file-plus</v-icon>
                </v-list-item-icon>
              </v-list-item>
            </v-list-group>
          </div>
          
          <template v-slot:append>
            <v-divider class="white mx-3" />
            <div class="pa-2">
              <v-btn text block color="white" @click="signOut">
                <v-icon left>mdi-out</v-icon>
                {{ $t('navbar.sign_out') }}
              </v-btn>
            </div>
          </template>
        </v-navigation-drawer>
        <!-- Show Footer -->
        <v-footer
          v-if="drawer"
          absolute
          padless 
        >
          <v-card
            flat
            tile
            width="100%"
            class="black lighten-1 text-center"
          >
            <v-card-text class="white--text">
              ກະຊວງໂຍທາທິການ ແລະຂົນສົ່ງ ສປປ.ລາວ — © Copyright {{ new Date().getFullYear() }} — <strong>CDG (Thailand) Ltd.</strong> - version 1.0.1.6
            </v-card-text>
          </v-card>
        </v-footer>
    </nav>
</template>

<script>
import firebase, { firestore } from "firebase"

export default {
  data () {
    return {
      loggedIn: false,
      user: '',
      appbar: true,
      drawer: false,
      prominent: true,
      permanent: false,
      drawerButton: false,
      languages: [
        {
          title: this.$t('languages.laos'),
          value: 'la'
        },
        {
          title: this.$t('languages.english'),
          value: 'us'
        }
      ]
    }
  },
  computed: {
    // Show Admin tab
    admin () {
      return [
        {title: this.$t('navbar.register'), icon: 'mdi-folder-account', index: true},
        {title: this.$t('navbar.license'), icon: 'mdi-file-document-outline', index: false} 
      ]
    },
    // Show Staff tab
    staff () {
      return [
        {title: this.$t('navbar.license'), icon: 'mdi-file-document-outline', index: false}
      ]
    },
    // Show Company tab
    company () {
      return [
        {title: this.$t('navbar.license'), icon: 'mdi-file-document-outline', link: '/staff_register_list', disabled: false, index: true}
      ]
    },
    // Show Logo tab
    logo_report () {
      return [
        {title: this.$t('navbar.logo_report'), icon: 'mdi-seal', link: '/staff_seal_report'}
      ]
    },
    // Set Show or Not at Page
    checkPage: function () {
      const page = this.$route.name
      if (page === 'Login' || page === 'Register' || page === 'User-Wait-Result') {
        return true
      } else {
        if (page === 'User-License-Report') {
          this.appbar = false
          this.drawer = false
        }  else {
          this.drawer = true
          this.appbar = true
        }
        return false
      }
    },
    isLogin: function () {
      const user = JSON.parse(localStorage.getItem('localUser'))
      const page = this.$store.state.currentPage.currentpage
      
      if (page === 'Login' || page === 'Register') {
        this.loggedIn = false
        return false
      } else {
        this.loggedIn = true
        this.user = user.username
        return true
      }
    },
    isCompany: function () {
      const page = this.$store.state.currentPage.currentpage
      if (page === 'Login' || page === 'Register') {
        this.drawer = false
        this.prominent = true
        return false
      } else {
        this.drawer = true
        this.prominent = false
        const type = JSON.parse(localStorage.getItem('localUser'))
        if (type.type === 'company') {
          return true
        } else {
          return false
        }
      }
    },
    isStaff: function () {
      const page = this.$store.state.currentPage.currentpage
      if (page === 'Login' || page === 'Register') {
        this.drawer = false
        this.prominent = true
        return false
      } else {
        this.drawer = true
        this.prominent = false
        const type = JSON.parse(localStorage.getItem('localUser'))
        if (type.type === 'staff') {
          return true
        } else {
          return false
        }
      }
    },
    isAdmin: function () {
      const page = this.$store.state.currentPage.currentpage
      if (page === 'Login' || page === 'Register') {
        this.drawer = false
        this.prominent = true
        return false
      } else {
        this.drawer = true
        this.prominent = false
        const type = JSON.parse(localStorage.getItem('localUser'))
        if (type.type === 'admin') {
          return true
        } else {
          return false
        }
      }
    }
  },
  created () {
    window.addEventListener("resize", this.onScreenChange);
  },
  destroyed () {
    window.removeEventListener("resize", this.onScreenChange);
  },
  // mounted: function () {
  //   const page = this.$route.name
  //   if (page === 'User-License-Report') {
  //     this.drawer = false
  //     this.appbar = false
  //   }
  // },
  methods: {
    changeLanguage (lang) {
      this.$i18n.locale = lang.value
      this.$store.dispatch('language/setLanguage', lang.value)
    },
    signOut () {
      localStorage.clear()
      this.$router.replace( { name: 'Login' } )
    },
    onScreenChange() {
      if (this.$route.name === 'Login' || this.$route.name === 'Register') {
        this.drawer = false
      } else {
        if (window.innerWidth < 991) {
          console.log(window.innerWidth)
          if (this.$route.name === 'Login' || this.$route.name === 'Register') {
            this.drawer = false
            this.drawerButton = false
          } else {
            this.drawerButton = true
          }
        } else {
          this.drawerButton = false
        }
      }
    },
    async openFile () {
      const fileName = 'ระบบขอใบอนุญาตนำเข้าทางด้านเทคนิค User.docx'

      await firebase.storage().ref(fileName).getDownloadURL().then(url => {
        window.open(url)
      })
    }
  }
}
</script>
  