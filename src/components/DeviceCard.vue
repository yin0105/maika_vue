<template>
    <vx-card>
        <div class="device-card">
            <div>
                <img :src="device.image" height="109px" class="mx-auto">
            </div>
            <div class="mt-4 mb-1 f-13-16">
                {{ device.type }}
            </div>
            <div class="mb-4 f-24-29-400">
                {{ device.location }}
            </div>
            <div class="flex justify-content-center">
                <b-button class="bottom-btn flex items-center">
                    <feather-icon icon="SettingsIcon" class="mr-2"/>
                    CONFIGURE
                </b-button>
            </div>
        </div>
    </vx-card>
</template>

<style>
    .device-card {
        padding: 2px 8px !important;
    }

    .vx-card__body {
        padding-top: 0px !important;
    }
</style>

<script>
export default {
  props: {
    device: { type: Object, default: false }
  }
}
</script>

<style lang="scss">
@import "@/assets/scss/vuexy/extraComponents/_form.scss"
</style>
