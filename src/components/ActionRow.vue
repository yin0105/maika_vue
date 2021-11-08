<template>
    <div class="mb-8">
        <div class="w-full flex items-center">
            <span class="text-nowrap mr-8 f-18-22 c-1">#{{ actionIndex + 1 }} Action</span>
            <v-select :options="actions" placeholder="select action to take" label="title" class="select-with-image w-full" @input="changeAction($event)" :value="actions[actionType]">
                <template slot="option" slot-scope="option">
                    <img :src="option.image" width="22px" height="22px"/>{{ option.title }}
                </template>
                <template slot="selected-option" slot-scope="option" :value="option.level">
                    <img :src="option.image" width="22px" height="22px" />{{ option.title }}
                </template>
            </v-select>
            <feather-icon icon="XCircleIcon" class="ml-4 cursor-pointer" :style="[{'color': '#C03221'}, actionIndex==0 ? {'visibility': 'hidden'}: {}]" @click="removeAction" />
        </div>
        <div v-if="actionType == 0">
            <action-one-row v-for="(one_row, index) in children" :key="index" :rowIndex="index" :content="one_row" :isLastIndex="index == children.length - 1" v-bind.sync="reaction" />
        </div>
    </div>
</template>

<script>
import vSelect from 'vue-select'
import ActionOneRow from './ActionOneRow.vue'

export default {
    data() {
        return {
            actions: [
                {
                  value: 0,
                  title:"MAIKA respond",
                  image: require('@/assets/images/svg/maika-respond.svg')
                },
                {
                  value: 1,
                  title:"Play Sound effect",
                  image: require('@/assets/images/svg/play-sound-effect.svg')
                },
                {
                  value: 2,
                  title:"Control IoT device",
                  image: require('@/assets/images/svg/control-iot-device.svg')
                },
                {
                  value: 3,
                  title:"Remind to-do list",
                  image: require('@/assets/images/svg/remind-to-do-list.svg')
                }
            ],
            reaction: {
                add: false,
                remove: -1,
                change: {
                    index: -1,
                    content: '',
                },
            },
            children: [""]  ,
            
             
        }
    },

    props: {
        actionIndex: { type: Number, required: true },
        actionType: { type: Number, required: true },
    },

    methods: {
        removeAction() {
            console.log("remove: ", this.actionIndex)
            this.$emit("update:remove", this.actionIndex);
        },
        changeAction: function (e) {
            this.$emit("update:change", this.actionIndex)
            this.$emit("update:changeAction", e.value)
        },
        getValidationState({ dirty, validated, valid = null }) {
            return dirty || validated ? valid : null;
        },
    },

    watch: {
        reaction: {
            handler: function (newReaction) {
                if (newReaction.add) {
                    newReaction.add = false
                    this.children.push("")
                }
                
                if (newReaction.remove > -1) {
                    this.children.splice(newReaction.remove, 1)
                    newReaction.remove = -1
                }

                if(newReaction.change.index > -1) {
                    this.children[newReaction.change.index] = newReaction.change.content
                    newReaction.change = {index: -1, content: ''}
                    console.log(this.children)
                }

            },
            deep: true,
        },
    },

    components: {
        'v-select': vSelect,
        'action-one-row': ActionOneRow,
    }
}
</script>

<style lang="scss">
// @import "@/assets/scss/vuexy/extraComponents/_routineRow.scss"
</style>
