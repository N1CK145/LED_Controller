<template>
    <div>
        <v-color-picker
            dot-size="25"
            mode="hexa"
            show-swatches
            hide-mode-switch
            v-model="currHexaColor"
            @update:color="onColorChange()"
            swatches-max-height="9000">
        </v-color-picker>
    </div>
</template>


<script>
export default {
    name: 'ColorPicker',

    data: () => ({
        currHexaColor: ''
    }),

    methods: {
        onColorChange(){
            this.$emit(
                'color-change',
                this.currHexaColor
            )
        }   
    },

    mounted: function() {
        this.currHexaColor = "#000000FF"
    }
}
</script>