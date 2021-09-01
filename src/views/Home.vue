<template>
  <main v-if="!loading">
    Show Data
  </main>
  <main class="flex flex-col align-center justify-center text-center"
  v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>


</template>

<script>
import CountrySelect from '@/components/CountrySelect';
import DataBoxes from '@/components/DataBoxes';
import DataTitle from '@/components/DataTitle';
import { ref } from 'vue';

export default {
  name: 'Home',
  components: {},
  data(){
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods: {
    async fetchCovidData (){
    const res = await fetch('https://api.covid19api.com/summary')
    const data = await res.json()
    return data
    }
  },
  async created(){
    const data = await this.fetchCovidData()


    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  }
}
</script>
