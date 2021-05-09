<template>
    <div v-if="!loading">
        <DataTitle :title="title" :dataDate="dataDate" />
        <DataBoxes :stats="stats" />
        <CountrySelect :countries="countries" @get-country="getCountryData" />

        <button
            @click="clearCountryData" 
            v-if="stats.Country"
            class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
            Clear Country
        </button>
    </div>

    <div class="flex flex-col align-center justify-center text-center" v-else>
        <div class="text-gray-500 text-3xl mt-10 mb-6">
            Fetching Data...
        </div>
        <img :src="loadingImage" class="w-24 m-auto">
    </div>
</template>

<script>
import DataTitle from '../components/DataTitle'
import DataBoxes from '../components/DataBoxes'
import CountrySelect from '../components/CountrySelect'

export default {
    name: 'Home',
    components: { DataTitle, DataBoxes, CountrySelect },
    data() {
        return {
            loading: true,
            title: "Global",
            dataDate: "",
            stats: [],
            countries: [],
            loadingImage: require('../assets/hourglass.gif')
        }
    },
    methods: {
        async fetchCovidData() {
            const res = await fetch('https://api.covid19api.com/summary')
            const data = await res.json()
            return data
        },
        getCountryData(country) {
            this.stats = country
            this.title = country.Country
        },
        async clearCountryData() {
            this.loading = true
            const data = await this.fetchCovidData()
            this.title = "Global"
            this.stats = data.Global
            this.loading = false
        }
    },
    async created() {
        const data = await this.fetchCovidData()
        console.log(data)

        this.loading = false
        this.dataDate = data.Date           // Inspect kısmından baktığımız zaman Date, Global, Countries gibi alanların olduğunu görebiliriz
        this.stats = data.Global
        this.countries = data.Countries
    }
}
</script>
