<template>
    <div>
        <v-color-picker
            dot-size="25"
            mode="hexa"
            show-swatches
            hide-mode-switch
            v-model="currHexaColor">
        </v-color-picker>
    </div>
</template>


<script>
export default {
    name: 'ColorPicker',

    data: () => ({
        currHexaColor: ''
    }),

    mounted: function() {
        this.currHexaColor = "#FF0000FF"
    }
}
</script>