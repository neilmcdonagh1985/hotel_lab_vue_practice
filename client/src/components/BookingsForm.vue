<template lang="html">
    <form id="bookings-form" v-on:submit="handleSubmit">
        <h2>Add a Booking</h2>
        <div>
        <label for="guestName">Guest Name</label>
        <input type="text" id="guestName" v-model="guestName"/>
        </div>
        <div>
        <label for="email">Email</label>
        <input type="text" id="email" v-model="email"/>
        </div>
        <div>
        <label for="checkedInStatus">Checked In</label>
        <input type="checkbox" id="checkedInStatus" v-model="checkedInStatus">
        <input type="submit" value="Save" id="save"/>

        </div>
    </form>
</template>

<script>
import { eventBus } from '../main';
import BookingsService from '../services/BookingsService.js';

export default {
    name: "bookings-form",
    data(){
        return {
            guestName: "",
            email: "",
            checkedInStatus: false
            
        }
        // $("checkedInStatus").prop( "checked", true);
    },
    methods: {
        handleSubmit(event){
            event.preventDefault();

            const payload = {
                guestName: this.guestName,
                email: this.email,
                checkedInStatus: this.checkedInStatus
            };

            BookingsService.postBooking(payload)
            .then(booking => eventBus.$emit('booking-added', booking))
                
            }
        }
    }

</script>

<style lang="css" scoped>

</style>