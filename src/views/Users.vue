<template>
  <div id="page-user-view">
    <div id="user-data" class="grid lg:grid-cols-12 lg:gap-20">
        <div class="lg:col-start-2 lg:col-span-5">    
          <vx-card title="Users" class="mb-base">
            <div class="grid grid-cols-11 gap-8">
              <div class="col-span-5">              
                <vs-input icon-pack="feather" icon="icon-search" placeholder="Search By User name" icon-no-border class="w-full"/>
              </div>
              <div class="col-span-3">              
                <v-select :options="['foo','bar']" placeholder="Filter by" />
              </div>
              <div class="col-span-3">              
                <vs-button color="warning" type="filled" icon-pack="feather" icon="icon-plus-circle" class="my-btn-primary">NEW USER</vs-button>
              </div>
              
            </div>
            
            <div>
              <ul class="mt-8">
                <li class="cursor-pointer" v-for="(contact, index) in contacts" :key="index">
                  <user-item :contact="contact"/>
                </li>
              </ul>
            </div>            
          </vx-card>
        </div>

        <!-- <div class="vx-col lg:w-1/3 w-full"> -->
        <div class="lg:col-start-7 lg:col-span-5"> 
          <vx-card title="Create New User" class="mb-base">
            <div id="card_container_2">
              <div class="grid grid-cols-10 gap-8 pt-2">
                <div class="col-span-3 flex items-center">              
                  Select Location
                </div>
                <div class="col-span-7">              
                  <v-select :options="['foo','bar']" placeholder="current of new office" />
                </div>                
              </div>              
              
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

const data = {
  
  chats: {
    1: {
      isPinned: true,
      msg: [
        {
          textContent: 'How can we help? We\'re here for you!',
          time: 'Mon Dec 10 2018 07:45:00 GMT+0000 (GMT)',
          isSent: true,
          isSeen: true
        },
        {
          textContent: 'Hey John, I am looking for the best admin template. Could you please help me to find it out?',
          time: 'Mon Dec 10 2018 07:45:23 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'It should be Bootstrap 4 compatible.',
          time: 'Mon Dec 10 2018 07:45:55 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'Absolutely!',
          time: 'Mon Dec 10 2018 07:46:00 GMT+0000 (GMT)',
          isSent: true,
          isSeen: true
        },
        {
          textContent: 'Modern admin is the responsive bootstrap 4 admin template.!',
          time: 'Mon Dec 10 2018 07:46:05 GMT+0000 (GMT)',
          isSent: true,
          isSeen: true
        },
        {
          textContent: 'Looks clean and fresh UI.',
          time: 'Mon Dec 10 2018 07:46:23 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'It\'s perfect for my next project.',
          time: 'Mon Dec 10 2018 07:46:33 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'How can I purchase it?',
          time: 'Mon Dec 10 2018 07:46:43 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'Thanks, from ThemeForest.',
          time: 'Mon Dec 10 2018 07:46:53 GMT+0000 (GMT)',
          isSent: true,
          isSeen: true
        },
        {
          textContent: 'I will purchase it for sure. 👍',
          time: 'Mon Dec 10 2018 07:47:00 GMT+0000 (GMT)',
          isSent: false,
          isSeen: false
        }
      ]
    },
    2: {
      isPinned: false,
      msg: [
        {
          textContent: 'Hi',
          time: 'Mon Dec 10 2018 07:45:00 GMT+0000 (GMT)',
          isSent: true,
          isSeen: true
        },
        {
          textContent: 'Hello. How can I help You?',
          time: 'Mon Dec 11 2018 07:45:15 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'Can I get details of my last transaction I made last month?',
          time: 'Mon Dec 11 2018 07:46:10 GMT+0000 (GMT)',
          isSent: true,
          isSeen: true
        },
        {
          textContent: 'We need to check if we can provide you such information.',
          time: 'Mon Dec 11 2018 07:45:15 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'I will inform you as I get update on this.',
          time: 'Mon Dec 11 2018 07:46:15 GMT+0000 (GMT)',
          isSent: false,
          isSeen: true
        },
        {
          textContent: 'If it takes long you can mail me at my mail address.',
          time: 'Mon Dec 11 2018 07:46:20 GMT+0000 (GMT)',
          isSent: true,
          isSeen: false
        }
      ]
    }
  }
}

export default {
  data () {
    return {
      user_data: null,
      user_not_found: false,
      contacts: [
        {
          uid: 1,
          displayName: 'Felecia Rower',
          position: 'Admin',
          photoURL: require('@/assets/images/portrait/small/avatar-s-1.jpg'),
          status: 'offline'
        },
        {
          uid: 2,
          displayName: 'Adalberto Granzin',
          position: 'Customer Service',
          photoURL: require('@/assets/images/portrait/small/avatar-s-2.jpg'),
          status: 'do not disturb'
        },
        {
          uid: 3,
          displayName: 'Joaquina Weisenborn',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-3.jpg'),
          status: 'do not disturb'
        },
        {
          uid: 4,
          displayName: 'Verla Morgano',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-4.jpg'),
          status: 'online'
        },
        {
          uid: 5,
          displayName: 'Margot Henschke',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-5.jpg'),
          status: 'do not disturb'
        },
        {
          uid: 6,
          displayName: 'Sal Piggee',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-6.jpg'),
          status: 'online'
        },
        {
          uid: 7,
          displayName: 'Miguel Guelff',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-7.jpg'),
          status: 'online'
        },
        {
          uid: 8,
          displayName: 'Mauro Elenbaas',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-8.jpg'),
          status: 'away'
        },
        {
          uid: 9,
          displayName: 'Bridgett Omohundro',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-9.jpg'),
          status: 'offline'
        },
        {
          uid: 10,
          displayName: 'Zenia Jacobs',
          position: 'Principle Engineer',
          photoURL: require('@/assets/images/portrait/small/avatar-s-10.jpg'),
          status: 'away'
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
  created () {
    return this.contacts.map(contact => {
      contact.status = contact.status == "online"? "#2DCA8C": "#FF715B";
      return contact;
      });
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
  },
  // beforeDestroy () {
  //   this.$store.unregisterModule('chat')
  // },
  // mounted () {
  //   this.$store.dispatch('chat/setChatSearchQuery', '')
  // },
  computed: {
    // contacts () {
    //   console.log("contact = ", this.$store.getters['chat/contacts'])
    //   return this.$store.getters['chat/contacts'].map(contact => {
    //     contact.status = contact.status == "online"? "#2DCA8C": "#FF715B";
    //     return contact;
    //   });
    // },
  },
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
  @import "@/assets/scss/vuexy/extraComponents/_button.scss";
  @import "@/assets/scss/vuexy/extraComponents/_select.scss";
</style>
