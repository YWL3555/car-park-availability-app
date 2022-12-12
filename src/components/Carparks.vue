<template>
  <div class="container">
    <button @click="sortCarparks">Click me to refresh manually</button>
    <b-container class="bv-example-row">
      <b-row>
        <b-col lg="3">
          <div>
      <h1> Small car parks:</h1>
        <div>
          <h2>Highest available:</h2>
          <div v-for="carpark in smallBCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
        <div>
          <h2>Lowest available:</h2>
          <div v-for="carpark in smallSCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
          </div>
        </b-col>
        <b-col lg="3">
          <div>
      <h1> Medium car parks:</h1>
        <div>
          <h2>Highest available:</h2>
          <div v-for="carpark in mediumBCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
        <div>
          <h2>Lowest available:</h2>
          <div v-for="carpark in mediumSCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
          </div>
        </b-col>
        <b-col lg="3">
          <div>
      <h1> Big car parks:</h1>
        <div>
          <h2>Highest available:</h2>
          <div v-for="carpark in bigBCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
        <div>
          <h2>Lowest available:</h2>
          <div v-for="carpark in bigSCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
          </div>
        </b-col>
        <b-col lg="3">
          <div>
      <h1> Large car parks:</h1>
        <div>
          <h2>Highest available:</h2>
          <div v-for="carpark in largeBCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
        <div>
          <h2>Lowest available:</h2>
          <div v-for="carpark in largeSCP" v-bind:key="carpark.carpark_number" style="background-color: white; margin-bottom: 5px" >
            <h5>Carpark: {{carpark.id}}</h5>
            <h5>total lot: {{carpark.total_lots}}</h5>
            <h5>available lot: {{carpark.lots_available}}</h5>
          </div>
        </div>
          </div>
        </b-col>
      </b-row>
    </b-container>
    
    
    
    
  </div> 
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Users',
    data() {
      return {
        carparks: null,
        smallS: 0,
        smallB: 0,
        mediumS: 0,
        mediumB: 0,
        bigS: 0,
        bigB: 0,
        largeS: 0,
        largeB: 0,
        smallSCP: [],
        smallBCP: [],
        mediumSCP: [],
        mediumBCP: [],
        bigSCP: [],
        bigBCP: [],
        largeSCP: [],
        largeBCP: [],
      };
    },
    methods: {
      sortCarparks(){
        this.resetData();
        this.carparks.forEach(carpark => {
          if (carpark.total_lots < 100){
            if (this.smallSCP.length < 1){
              this.smallS = carpark.lots_available;
              this.smallB = carpark.lots_available;
              this.smallSCP.push(carpark);
              this.smallBCP.push(carpark);
            } else {
              if (carpark.lots_available <= this.smallS){
                if (carpark.lots_available == this.smallS){
                  //Append
                  this.smallSCP.push(carpark);
                } else {
                  this.smallS = carpark.lots_available;
                  this.smallSCP = [carpark];
                }
              }
              if (carpark.lots_available >= this.smallB){
                if (carpark.lots_available == this.smallB){
                  //Append
                  this.smallBCP.push(carpark);
                } else {
                  this.smallB = carpark.lots_available;
                  this.smallBCP = [carpark];
                }
              }
            }
          } else if (carpark.total_lots < 300){
            if (this.mediumSCP.length < 1){
              this.mediumS = carpark.lots_available;
              this.mediumB = carpark.lots_available;
              this.mediumSCP.push(carpark);
              this.mediumBCP.push(carpark);
            } else {
              if (carpark.lots_available <= this.mediumS){
                if (carpark.lots_available == this.mediumS){
                  //Append
                  this.mediumSCP.push(carpark);
                } else {
                  this.mediumS = carpark.lots_available;
                  this.mediumSCP = [carpark];
                }
              }
              if (carpark.lots_available >= this.mediumB){
                if (carpark.lots_available == this.mediumB){
                  //Append
                  this.mediumBCP.push(carpark);
                } else {
                  this.mediumB = carpark.lots_available;
                  this.mediumBCP = [carpark];
                }
              }
            }
          } else if (carpark.total_lots < 400){
            if (this.bigSCP.length < 1){
              this.bigS = carpark.lots_available;
              this.bigB = carpark.lots_available;
              this.bigSCP.push(carpark);
              this.bigBCP.push(carpark);
            } else {
              if (carpark.lots_available <= this.bigS){
                if (carpark.lots_available == this.bigS){
                  //Append
                  this.bigSCP.push(carpark);
                } else {
                  this.bigS = carpark.lots_available;
                  this.bigSCP = [carpark];
                }
              }
              if (carpark.lots_available >= this.bigB){
                if (carpark.lots_available == this.bigB){
                  //Append
                  this.bigBCP.push(carpark);
                } else {
                  this.bigB = carpark.lots_available;
                  this.bigBCP = [carpark];
                }
              }
            }
          } else {
            if (this.largeSCP.length < 1){
              this.largeS = carpark.lots_available;
              this.largeB = carpark.lots_available;
              this.largeSCP.push(carpark);
              this.largeBCP.push(carpark);
            } else {
              if (carpark.lots_available <= this.largeS){
                if (carpark.lots_available == this.largeS){
                  //Append
                  this.largeSCP.push(carpark);
                } else {
                  this.largeS = carpark.lots_available;
                  this.largeSCP = [carpark];
                }
              }
              if (carpark.lots_available >= this.largeB){
                if (carpark.lots_available == this.largeB){
                  //Append
                  this.largeBCP.push(carpark);
                } else {
                  this.largeB = carpark.lots_available;
                  this.largeBCP = [carpark];
                }
              }
            }
          }
        });
      },
      resetData(){
        this.smallS = 0;
        this.smallB = 0;
        this.mediumS = 0;
        this.mediumB = 0;
        this.bigS = 0;
        this.bigB = 0;
        this.largeS = 0;
        this.largeB = 0;
        this.smallSCP = [];
        this.smallBCP = [];
        this.mediumSCP = [];
        this.mediumBCP = [];
        this.bigSCP = [];
        this.bigBCP = [];
        this.largeSCP = [];
        this.largeBCP = [];
      }
    },
    created: function() {
      
    },
    mounted: async function() {
      var cp = await axios
        .get('https://api.data.gov.sg/v1/transport/carpark-availability')
        .then(res => {
          this.carparks = res.data.items[0].carpark_data.map((carpark)=>{
            return {
              id: carpark.carpark_number,
              total_lots: carpark.carpark_info[0].total_lots,
              lots_available: carpark.carpark_info[0].lots_available
            }
          });
        });
      this.sortCarparks();
      window.setInterval(() => {
          this.sortCarparks()
        }, 60000);
    }
  }
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>