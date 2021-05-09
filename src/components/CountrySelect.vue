<template>
    <select 
        @change="onChange"
        v-model="selected" 
        class="form-select mt-10 block w-full border p-3 rounded "
    >
        <option value="0">Select Country</option>
        <option v-for="country in countries" :value="country.ID" :key="country.ID">
            {{ country.Country }}
        </option>
    </select>
</template>

<script>
export default {
    props: ['countries'],
    data() {
        return {
            selected: 0
        }
    },
    methods: {
        onChange() {
            const country = this.countries.find(item => item.ID === this.selected)
            console.log(country)
            this.$emit('get-country', country)       // Home.vue'ya "get-country" adında country emitini yolluyoruz
        }
    }
}
</script>
