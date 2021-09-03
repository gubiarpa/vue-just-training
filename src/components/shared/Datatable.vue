<template>
    <div class="mx-4 my-4">
        <v-data-table
            :headers="headers"
            :items="items"
            :items-per-page="10"
            class="elevation-1"
        ></v-data-table>
    </div>
</template>

<script>
  export default {
    data () {
      return {
        headers: [
            {
                text: 'Country',
                align: 'start',
                sortable: false,
                value: 'name',
            },
            { text: 'Capital', value: 'capital' },
            { text: 'Region', value: 'region' },
            { text: 'Subregion', value: 'subregion' },
            { text: 'Population', value: 'population' },
            { text: 'Area', value: 'area' },
        ],
        items: [],
      }
    },
    methods: {
        loadCountries () {
            fetch('https://restcountries.eu/rest/v2/all')
                .then(response => response.json())
                .then(data => {
                    data.forEach(country => {
                        this.items.push({
                            name: country.name,
                            capital: country.capital,
                            region: country.region,
                            subregion: country.subregion,
                            population: country.population,
                            area: country.area,
                        })
                    })
                })
        },
        
    },
    mounted () {
        this.loadCountries()
    },
  }
</script>