<template>
    <div style="margin: 20px">
        <dropdown :options="objects" :selected="selected" v-on:updateOption="onSelect"></dropdown>
    </div>
</template>

<script>
import dropdown from 'vue-dropdowns'

export default {
    name: "Dropdown",

    data() {
        return {
            objects: [
                { name: "TV", value: "E0:98:06:86:3A:47" },
                { name: "Test", value: "Test" }
            ],
            selected: {
                name: "TV",
                value: "E0:98:06:86:3A:47"
            }
        }
    },
    components: {
        dropdown
    },
    methods: {
        onSelect(payload){
            this.selected = payload
            this.$emit(
                "host-change",
                this.selected.value
            )
        }
    }
}
</script>