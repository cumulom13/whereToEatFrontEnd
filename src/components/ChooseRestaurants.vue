<template>
 <div>
   <div class="col-md-12">
    <Restaurant  v-for="restaurant in listOfRestaurants" v-bind:key="restaurant.id" v-bind:id="restaurant.id" v-bind:restaurantName="restaurant.name" />
   </div>
    <button type="button" @click="alter()">
            Choose a Restaurant!!!
    </button>
 </div>
</template>


<script>
import axios from "axios";
import Restaurant from './Restaurant'


export default {
    name: 'ChooseRestaurant',
    data() {
        return {
            listOfRestaurants: []
        }
    },    
    components: {
        Restaurant
    },
    created: function () {
          
        axios.get('http://localhost:8080/getAllRestaurants')
        .then(response => {
            this.listOfRestaurants = response.data
        })   
    },
 
    methods: {
        createAvailableRestaurantsIdList: function(){
            var restaurantsIds = [];

            var restaurantsToExclude = [];

            document.querySelectorAll(".deactivate").forEach(element => {
                let restaurantName = element.querySelector("h1").innerHTML;
                restaurantsToExclude.push(restaurantName)
            })

            var localListOfRestaurants = this.listOfRestaurants.slice(0);

            for(let i = 0; i<restaurantsToExclude.length; i++){
                for(let j = 0; j < localListOfRestaurants.length; j++){
                    if(restaurantsToExclude[i] === localListOfRestaurants[j].name){
                        localListOfRestaurants.splice(j, 1);
                    }
                }
            }

            localListOfRestaurants.forEach(element => {
                restaurantsIds.push(element.id);
            });     
            
            return restaurantsIds
        },

        
        removeDuplicates: function removeDuplicateUsingFilter(arr){
            let unique_array = arr.filter(function(elem, index, self) {
                return index == self.indexOf(elem);
            });
            return unique_array
        },

        alter: function() {
            var restaurantsIds = this.createAvailableRestaurantsIdList();

            var URL = 'http://localhost:8080/randomRestaurant/' + restaurantsIds;
            
            axios.get(URL).then(response => {
                alert(response.data.name)
            })
        }
    }
}
</script>