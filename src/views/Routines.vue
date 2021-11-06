<template>
  <div id="page-user-view">

    <div id="user-data" class="grid lg:grid-cols-11 lg:gap-10">
        <div class="lg:col-span-2">    
          <vx-card title="Users/Location" class="mb-base px0">
            <div class="sub-title px-4">
                Type of targeted entity
            </div>  
            <v-select :options="['User','Location']" class="px-4" />
            <div v-if="targetedEntityType == 'User'"  class="px-4 flex mt-6 items-center">
                <span class="w-2/5 c-1">Filter by</span>
                <v-select :options="['User','Location']" class="w-3/5 "/>
            </div>
            <div class="mt-8 mb-2">
              <ul>
                <li class="cursor-pointer" v-for="(contact, index) in contacts" :key="index">
                  <user-item :contact="contact" :narrow="narrow"/>
                </li>
              </ul>
            </div>
            <div class="mt-12">
              <b-button variant="primary" class="bottom-btn create flex items-center mx-auto">
                <feather-icon icon="PlusCircleIcon"/>
                Choose
              </b-button>
            </div>
          </vx-card>
        </div>
<!-- 2nd Column -->
        <div class="lg:col-span-4">    
          <vx-card title="Trigger Condition" class="mb-base pr-12">
            <div class="w-full flex items-center">
              <span class="text-nowrap mr-8 f-18-22 c-1">Via Device</span>
              <v-select :options="options" label="title" class="select-with-image w-full">
                <template slot="option" slot-scope="option">
                    <img :src="option.image" width="22px" height="22px"/>{{ option.title }}
                </template>
                <template slot="selected-option" slot-scope="option" :value="option.level">
                  <img :src="option.image" width="22px" height="22px" />{{ option.title }}
                </template>
              </v-select>
            </div>

            <div class="f-18-22 h-29 mt-4 c-1">
              when <span class="c-b">Lí Nguyễn</span>
            </div>

            <div>
              <p-check name="check" color="success" v-model="check">Check</p-check>
              <p-check class="p-svg p-curve" color="success">
                <!-- svg path -->
                <svg width="12" height="9" viewBox="0 0 12 9" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M0.387465 5.60626C-0.129155 5.12354 -0.129155 4.3409 0.387465 3.85818C0.904084 3.37547 1.74169 3.37547 2.25831 3.85818L3.94207 5.43145C4.04539 5.52799 4.21292 5.52799 4.31624 5.43145L9.74169 0.362038C10.2583 -0.120679 11.0959 -0.120679 11.6125 0.362038C12.1292 0.844755 12.1292 1.62739 11.6125 2.11011L4.31624 8.92759C4.21292 9.02414 4.04539 9.02414 3.94207 8.92759L0.387465 5.60626Z" fill="#3A57E8"/>
                </svg>
                Recurring
            </p-check>
             <p-check class="p-svg p-plain">
                <svg width="12" height="9" viewBox="0 0 12 9" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M0.387465 5.60626C-0.129155 5.12354 -0.129155 4.3409 0.387465 3.85818C0.904084 3.37547 1.74169 3.37547 2.25831 3.85818L3.94207 5.43145C4.04539 5.52799 4.21292 5.52799 4.31624 5.43145L9.74169 0.362038C10.2583 -0.120679 11.0959 -0.120679 11.6125 0.362038C12.1292 0.844755 12.1292 1.62739 11.6125 2.11011L4.31624 8.92759C4.21292 9.02414 4.04539 9.02414 3.94207 8.92759L0.387465 5.60626Z" fill="#3A57E8"/>
                </svg>
                Done
            </p-check>

             <p-check class="pretty p-image p-plain">
                <svg width="12" height="9" viewBox="0 0 12 9" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd" d="M0.387465 5.60626C-0.129155 5.12354 -0.129155 4.3409 0.387465 3.85818C0.904084 3.37547 1.74169 3.37547 2.25831 3.85818L3.94207 5.43145C4.04539 5.52799 4.21292 5.52799 4.31624 5.43145L9.74169 0.362038C10.2583 -0.120679 11.0959 -0.120679 11.6125 0.362038C12.1292 0.844755 12.1292 1.62739 11.6125 2.11011L4.31624 8.92759C4.21292 9.02414 4.04539 9.02414 3.94207 8.92759L0.387465 5.60626Z" fill="#3A57E8"/>
                </svg>
                Agree
            </p-check>

              <p-check class="p-icon p-round p-smooth" color="success">
                  <i slot="extra" class="icon mdi mdi-check">
                  <feather-icon icon="XIcon" svgClasses="h-4 w-4 cursor-pointer text-danger" class="hover:text-danger"/>
                  </i>
                  Tuesday
              </p-check>

              <p-check class="p-icon p-smooth" color="my-primary">
                  <!-- <i slot="extra" class="icon mdi mdi-close"></i> -->
                  <i slot="extra" class="icon mdi mdi-check">
                  <feather-icon icon="CheckIcon" svgClasses="h-4 w-4 cursor-pointer text-success" class="hover:text-danger"/>
                  </i>
                  Wednesday
              </p-check>
            </div>

            <!-- <div class="w-full flex">
              <input type="checkbox">
            </div>

            <label class="checkbox">
              <input type="checkbox" />
              <span>Check Me</span>
            </label> -->
          </vx-card>
        </div>

        <div class="lg:col-span-5">    
          <vx-card title="All Routines" class="mb-base">
            <div class="grid grid-cols-2">
                  asdaf          
            </div>            
          </vx-card>
        </div>
      </div>
  </div>
</template>

<script>
import moduleUserManagement from '@/store/user-management/moduleUserManagement.js'
import vSelect from 'vue-select'
import UserItem from '../components/UserItem.vue'
import moduleChat          from '@/store/chat/moduleChat.js'
import { contacts } from './data'

export default {
  data () {
    return {
      user_data: null,
      user_not_found: false,
      targetedEntityType: 'User',
      contacts: contacts,
      narrow: true,
      reconigedByCamera: true,
      options: [
                {
                  level: 1,
                  title:"Camera HANET - Entry Door",
                  image: require('@/assets/images/svg/camera.svg')
                },
                {
                  level: 2,
                  title:"Image 2",
                  image: require('@/assets/images/portrait/small/avatar-s-5.jpg')
                },
                {
                  level: 3,
                  title:"Image 3",
                  image: require('@/assets/images/portrait/small/avatar-s-4.jpg')
                }
              ],
    }
  },
  computed: {
    userAddress () {
      let str = ''
      for (const field in this.user_data.location) {
        str += `${field  } `
      }
      return str
    }
  },
  methods: {
    confirmDeleteRecord () {
      this.$vs.dialog({
        type: 'confirm',
        color: 'danger',
        title: 'Confirm Delete',
        text: `You are about to delete "${this.user_data.username}"`,
        accept: this.deleteRecord,
        acceptText: 'Delete'
      })
    },
    deleteRecord () {
      /* Below two lines are just for demo purpose */
      this.$router.push({name:'app-user-list'})
      this.showDeleteSuccess()

      /* UnComment below lines for enabling true flow if deleting user */
      this.$store.dispatch("userManagement/removeRecord", this.user_data.id)
        .then(()   => { this.$router.push({name:'app-user-list'}); this.showDeleteSuccess() })
        .catch(err => { console.error(err)       })
    },
    showDeleteSuccess () {
      this.$vs.notify({
        color: 'success',
        title: 'User Deleted',
        text: 'The selected user was successfully deleted'
      })
    }
  },
  // created () {
  //   // Register Module UserManagement Module
  //   this.$store.registerModule('chat', moduleChat)
  //   this.$store.dispatch('chat/fetchContacts')
  //   if (!moduleUserManagement.isRegistered) {
  //     this.$store.registerModule('userManagement', moduleUserManagement)
  //     moduleUserManagement.isRegistered = true
  //   }

  //   const userId = this.$route.params.userId
  //   this.$store.dispatch('userManagement/fetchUser', '268')
  //     .then(res => { this.user_data = res.data })
  //     .catch(err => {
  //       if (err.response.status === 404) {
  //         this.user_not_found = true
  //         return
  //       }
  //       console.error(err) 
  //     })
  // },
  // beforeDestroy () {
  //   this.$store.unregisterModule('chat')
  // },
  // mounted () {
  //   this.$store.dispatch('chat/setChatSearchQuery', '')
  // },
  // computed: {
  //   contacts () {
  //     console.log("contact = ", this.$store.getters['chat/contacts'])
  //     return this.$store.getters['chat/contacts'].map(contact => {
  //       contact.status = contact.status == "online"? "#2DCA8C": "#FF715B";
  //       return contact;
  //     });
  //   },
  // },
  components: {
    'v-select': vSelect,
    'user-item': UserItem
  }
}

</script>

<style lang="scss">
#avatar-col {
  width: 10rem;
}

#page-user-view {
  table {
    td {
      vertical-align: top;
      min-width: 140px;
      padding-bottom: .8rem;
      word-break: break-all;
    }

    &:not(.permissions-table) {
      td {
        @media screen and (max-width:370px) {
          display: block;
        }
      }
    }
  }
}

#card_container_2 {
  margin-left: 17px;
  margin-right: 17px;
}
// #account-info-col-1 {
//   // flex-grow: 1;
//   width: 30rem !important;
//   @media screen and (min-width:1200px) {
//     & {
//       flex-grow: unset !important;
//     }
//   }
// }


@media screen and (min-width:1201px) and (max-width:1211px),
only screen and (min-width:636px) and (max-width:991px) {
  #account-info-col-1 {
    width: calc(100% - 12rem) !important;
  }

  // #account-manage-buttons {
  //   width: 12rem !important;
  //   flex-direction: column;

  //   > button {
  //     margin-right: 0 !important;
  //     margin-bottom: 1rem;
  //   }
  // }

}

</style>

<style lang="scss">
  @import "@/assets/scss/vuexy/extraComponents/_form.scss";
  @import "@/assets/scss/vuexy/extraComponents/_button.scss";
  @import "@/assets/scss/vuexy/extraComponents/_select.scss";
</style>
