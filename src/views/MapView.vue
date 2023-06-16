<template>
    <div class="pt-6">
        <h1 class="text-3xl font-semibold mb-4">Here's your trip</h1>
        <div>
            <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
                <div class="bg-white px-4 py-5 sm:p-6">
                    <div>
                        <GMapMap :zoom="11" :center="location.destination.geometry" 
                        style="height: 256px; width: 100%;">
                        <GMapMarker :position="location.destination.geometry"></GMapMarker>
                    </GMapMap>
                    </div>
                    <div class="mt-2">
                        <p class="text-xl">Going to <srong>{{location.destination.name}}</srong></p>
                    </div>
                </div>
                <div class="bg-gray-50 px-4 py-3 text-right sm:px-6">
                    <button @click="checkValues" class="inline-flex justify-center rounded-md border border-transparent bg-black py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-gray-600 focus:outline-none">
                        Let's Go!
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { useLocationStore } from '../stores/location';
import { useRouter } from 'vue-router';
import { onMounted } from 'vue';

const location = useLocationStore()
const router = useRouter()


onMounted(() => {
    if (location.destination.name == '') {
        router.push({
            name: 'location'
        })
    }

    // get current users location
    navigator.geolocation.getCurrentPosition((success) => {
        console.log('Your current location is:', success);
    }, (error) => {
        console.error(error);
    })
})
const checkValues = () => {
    console.log('This is the geometry:',location.destination.geometry);
}
</script>
<style>
    
</style>