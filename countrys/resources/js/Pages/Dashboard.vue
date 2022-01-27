<template>
    <Head title="Dashboard" />

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        
                        <div class="flex">

                            <div class="w-1/2">
                                MAP
                            </div>
                            <div class="w-1/2 relative">
                              <div class="block bg-white shadow rounded relative p-3">
                                <h3>Visited Countries</h3>
                                <Select2 
                                v-model="visitedCountry" 
                                :settings="{ width: '80%', 
                                ajax: { 
                                     url: '/api/countries/list',
                                     dataType: 'json'
                                     } 
                                }" 
                                @select="selectVisitedCountry($event)" 
                                />
                                <a @click="addVisitedCountry" class="rounded bg-green-300 hover:bg-green-400 px-4 py-1 shadow pointer
                                    absolute right-3 top-8
                                ">Add</a>
                                <br />
                                <div v-for="country in visitedCountries" :key="country.id"
                                    class = "p-2 border-b-2 relative"
                                >
                                    {{ country.name }}
                                    <a href="javascript:void(0)"
                                    @click="removeVisitedCountry(country.id)"
                                    class="absolute right-1 top-2"
                                    ><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAABmJLR0QA/wD/AP+gvaeTAAADhklEQVRoge2Yv6sdRRTHP2f3hQh5aiNCXoIpHkFjYSD4J4hFbOyE/AF2EqzS2gaEtObPsNJCaxvRQsSo7yUQQrgbEoMkgWe4u1+Lu7M7+/PO3N1bBO4p7p3ZOWfmc2bnzJlZ2MlOdvJKi03u4cavnxh2G3Eu0vKBLPmcmx98N2X4ZIoxgMm+2QAe4LypuD15/GiLr37f5yR5l8QOMQ7I81tgYFb25ro0QD1llUWBBGn6JeIhhY5ZvrzD15dfzOfAjeM32cs/An0IuoJ4D+ydmAEiRcB9TH+C/QL2M8v0B24e/jtksDfaXbr8CXFpVZkeLgFiwAVkF4CPQZAu/wDeHzIYjwHj3rx8G8ndscagab3y49Mj4HCdnlSV6qVeVps68tUaOqofHv129a2L68YM3YWysUbJA5NWdQclX0cVdVtHaNVe6Wt0TCfjMTDmgD97AzMuR95n051xmuo2nwOGZep97fJZZgJ3+jO+AaFsE/A2VCC4ez6rA4suaIttErg6k4FYhLCFLaHcMpm64K0H3dlsFILAq73AZoyBIi0y8nrHHdwKZwB3NVHM50CudJFShO3hg1CB4HVfcy6hk0ycGgfvxMRm4K7x9Gs8CmILUQK4/P2T54Izo+Bq2khtr3xwdW3q7p7f+fTt10O4gu8DQovhrOmBaAUuecSlquqfHhtvN1PY8olywLRKZmvBK9oaKgLc6QcFMIQfJSi8s0n8juLXacWROjZac/byJdgBwWJSYJZtY+De4+AlFOwAssy989gdpZknxsBdh2FJDGIcKIpMbs+KBfePGQ2bNnjVvgUHsKx/9taDd2KAAfCybLYNByzPpGQaeKXTD+7+VGzBAYNFBRYJ3r5qNpqret2WbiOI7ZQynXiJewq4r9OTzU//F3aMgMhvJZe+ffQMsR8L3p7tIfBSnh1/dvaNUKaIIAZEJtgP2woHwFvJoWc5Bq9/iPw2Kinz0n3NKgcmlypq58py+3w0fAwJuws72eQNeA45SnpnXLXSiE4zqovINxDlgMQCiwfv3pF7rqfljwVeZJzEOQBVMpsNvBESio6BOAeMzIp48PYy6ep45yvbYgyYi4Ge5NOF6oK3Z7/3c0qRbM+BImdhth3wKgas2F4MJMv872LPciDdBDzgjpy/TJKjKKYY5b+uHTxGXJd4OnqVxM8TCr0j/1PAFw+vHTyOYdrJTnbyisv/NadhxosNDcEAAAAASUVORK5CYII="/></a>    
                                </div>
                              </div> 
                              <div class="block bg-white shadow rounded relative p-3 p-3 mt-6">
                                <h3>to Visit Countries</h3>
                                <Select2 
                                v-model="toVisitCountry" 
                                :settings="{ width: '80%', 
                                ajax: { 
                                     url: '/api/countries/list',
                                     dataType: 'json'
                                     } 
                                }" 
                                @select="selectToVisitCountry($event)" 
                                />
                                <a @click="addToVisitCountry" class="rounded bg-green-300 hover:bg-green-400 px-4 py-1 shadow pointer
                                    absolute right-3 top-8
                                ">Add</a>
                                <br />
                                <div v-for="country in toVisitCountries" :key="country.id"
                                    class = "p-2 border-b-2 relative"
                                >
                                    {{ country.name }}
                                    <a href="javascript:void(0)"
                                    @click="removeToVisitCountry(country.id)"
                                    class="absolute right-1 top-2"
                                    ><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAABmJLR0QA/wD/AP+gvaeTAAADhklEQVRoge2Yv6sdRRTHP2f3hQh5aiNCXoIpHkFjYSD4J4hFbOyE/AF2EqzS2gaEtObPsNJCaxvRQsSo7yUQQrgbEoMkgWe4u1+Lu7M7+/PO3N1bBO4p7p3ZOWfmc2bnzJlZ2MlOdvJKi03u4cavnxh2G3Eu0vKBLPmcmx98N2X4ZIoxgMm+2QAe4LypuD15/GiLr37f5yR5l8QOMQ7I81tgYFb25ro0QD1llUWBBGn6JeIhhY5ZvrzD15dfzOfAjeM32cs/An0IuoJ4D+ydmAEiRcB9TH+C/QL2M8v0B24e/jtksDfaXbr8CXFpVZkeLgFiwAVkF4CPQZAu/wDeHzIYjwHj3rx8G8ndscagab3y49Mj4HCdnlSV6qVeVps68tUaOqofHv129a2L68YM3YWysUbJA5NWdQclX0cVdVtHaNVe6Wt0TCfjMTDmgD97AzMuR95n051xmuo2nwOGZep97fJZZgJ3+jO+AaFsE/A2VCC4ez6rA4suaIttErg6k4FYhLCFLaHcMpm64K0H3dlsFILAq73AZoyBIi0y8nrHHdwKZwB3NVHM50CudJFShO3hg1CB4HVfcy6hk0ycGgfvxMRm4K7x9Gs8CmILUQK4/P2T54Izo+Bq2khtr3xwdW3q7p7f+fTt10O4gu8DQovhrOmBaAUuecSlquqfHhtvN1PY8olywLRKZmvBK9oaKgLc6QcFMIQfJSi8s0n8juLXacWROjZac/byJdgBwWJSYJZtY+De4+AlFOwAssy989gdpZknxsBdh2FJDGIcKIpMbs+KBfePGQ2bNnjVvgUHsKx/9taDd2KAAfCybLYNByzPpGQaeKXTD+7+VGzBAYNFBRYJ3r5qNpqret2WbiOI7ZQynXiJewq4r9OTzU//F3aMgMhvJZe+ffQMsR8L3p7tIfBSnh1/dvaNUKaIIAZEJtgP2woHwFvJoWc5Bq9/iPw2Kinz0n3NKgcmlypq58py+3w0fAwJuws72eQNeA45SnpnXLXSiE4zqovINxDlgMQCiwfv3pF7rqfljwVeZJzEOQBVMpsNvBESio6BOAeMzIp48PYy6ep45yvbYgyYi4Ge5NOF6oK3Z7/3c0qRbM+BImdhth3wKgas2F4MJMv872LPciDdBDzgjpy/TJKjKKYY5b+uHTxGXJd4OnqVxM8TCr0j/1PAFw+vHTyOYdrJTnbyisv/NadhxosNDcEAAAAASUVORK5CYII="/></a>    
                                </div>
                              </div> 
                            </div>

                        </div>


                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>

<script>
import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue'
import { Head } from '@inertiajs/inertia-vue3';
import Select2 from 'vue3-select2-component';

export default {
    components: {
        BreezeAuthenticatedLayout,
        Head,
        Select2
    },
       data() {
        return {
            visitedCountry: '',
            toVisitCountry: '',
            visitedCountries: [],
            toVisitCountries: []
        }
    },
    methods: {
        selectVisitedCountry({id, text}){
            console.log({id, text})
        },
        selectToVisitCountry({id, text}){
            console.log({id, text})
        },
        addVisitedCountry(){
            if(this.visitedCountry !== "")
            {
                axios.post("/api/add-visited-country", 
                {
                    countryID: this.visitedCountry
                }
                ).then((response) => {
                    this.getVisitedCountries();
                    console.log(response.data);
                    //@todo set color on the map for the country
                });
            }else{
                console.log("country is not selected from selector!");
            }

        },
        addToVisitCountry(){
                      if(this.toVisitCountry !== "")
            {
                axios.post("/api/add-country-to-visit", 
                {
                    countryID: this.toVisitCountry
                }
                ).then((response) => {
                    this.getToVisitCountries();
                    console.log(response.data);
                    //@todo set color on the map for the country
                });
            }else{
                console.log("country is not selected from selector!");
            }  
        },
        removeVisitedCountry(countryID){
            axios.delete("/api/remove-visited-country/"+countryID)
            .catch(function(error){
                console.log(error);
            }).then(() => {
                this.getVisitedCountries();
            });
        },
        removeToVisitCountry(countryID){
            axios.delete("/api/remove-to-visit-country/"+countryID)
            .catch(function(error){
                console.log(error);
            }).then(() => {
                this.getToVisitCountries();
            });
        },
        getVisitedCountries(){
            axios.get("/api/countries/visited")
                .then((response) => {
                    this.visitedCountries = response.data;
                });
        },
        getToVisitCountries(){
            axios.get("/api/countries/tovisit")
                .then((response) => {
                    this.toVisitCountries = response.data;
                });
        }
    },

    created(){
        this.getVisitedCountries();
    }

}
</script>
