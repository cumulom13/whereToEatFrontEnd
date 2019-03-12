<template>
    <div class="col-md-4">
        <div class="restaurant" v-bind:class="{deactivate: isDeactivate}" @click="addRemoveRestaurant">
            <h1>{{restaurantName}}</h1> 
        </div>
    </div>
</template>

<script>
import Vuex from 'vuex'



export default {
    name: 'Restaurant',
    props: {
        id: Number,
        restaurantName : String,
    },
    data() {
        return {
            isDeactivate: false
        }
    },
  
    // computed: {
    //     trial(){
    //         this.$store.state.trial = this.$store.state.trial
    //     }
    // },
    methods: {
        addRemoveRestaurant: function(){
         this.isDeactivate = !this.isDeactivate;            
        },
        tellMeHowYouAre: function(){
            return this.isDeactivate
        }
    }
}

</script>

<style>
.restaurant {
    border:2px solid tomato;
    border-radius: 4px;
    margin: 20px 0px;
}

.deactivate {
    background-color: dimgray;
}
</style>