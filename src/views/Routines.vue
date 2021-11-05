<template>
  <div id="page-user-view">

    <div id="user-data" class="grid lg:grid-cols-11 lg:gap-10">
        <div class="lg:col-span-2">    
          <vx-card title="Users/Location" class="mb-base narrow">
            <div class="sub-title px-4">
                Type of targeted entity
            </div>  
            <v-select :options="['User','Location']" class="px-4" />
            <div v-if="targetedEntityType == 'User'"  class="px-4 flex mt-6 items-center">
                <span class="w-2/5">Filter by</span>
                <v-select :options="['User','Location']" class="w-3/5 "/>
            </div>
            <div class="mt-8 mb-2">
              <ul>
                <li class="cursor-pointer" v-for="(contact, index) in contacts" :key="index">
                  <user-item :contact="contact" narrow="true"/>
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

        <div class="lg:col-span-4">    
          <vx-card title="Trigger Condition" class="mb-base">
            <div class="grid grid-cols-2">
                  asdaf          
            </div>            
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
