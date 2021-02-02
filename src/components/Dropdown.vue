<template>
    <div>
        <dropdown :options="objects" :selected="selected" @select="onSelect"></dropdown>
    </div>
</template>

<script>
import dropdown from 'vue-dropdowns'

export default {
    name: "Dropdown",

    data() {
        return {
            objects: [],
            selected: {
                name: "Hola",
                value: "asdasd"
            }
        }
    },
    components: {
        dropdown
    },
    methods: {
        onSelect(payload){
            this.selected = payload;
        }
    }
}
</script>