<template>
  <div class="container">
    <h1>Car Parks</h1>
    <h5>last updated: {{lastUpdated}}</h5>
    <button @click="sortCarparks">Click me to refresh manually</button>
    <div class="row" v-if="carparks">
  <div class="column-4"><div>
      <h1> Small car parks:</h1>
        <div class="column-2">
          
          <h2>Highest available ({{smallBCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in smallBCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        
        </div>
        <div class="column-2">
          <h2>Lowest available ({{smallSCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in smallSCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        </div>
          </div></div>
  <div class="column-4"><div>
        <h1> Medium car parks:</h1>
        <div class="column-2">
          
          <h2>Highest available ({{mediumBCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in mediumBCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        
        </div>
        <div class="column-2">
          <h2>Lowest available ({{mediumSCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in mediumSCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        </div>
          </div></div>
  <div class="column-4"><div>
      <h1> Big car parks:</h1>
      <div class="column-2">
          
          <h2>Highest available ({{bigBCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in bigBCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        
        </div>
        <div class="column-2">
          <h2>Lowest available ({{bigSCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in bigSCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        </div>
          </div></div>
  <div class="column-4"><div>
      <h1> Large car parks:</h1>
      <div class="column-2">
          
          <h2>Highest available ({{largeBCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in largeBCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        
        </div>
        <div class="column-2">
          <h2>Lowest available ({{largeSCP.length}})</h2>
          <table>
            <tr>
              <th>No.</th>
              <th>Total lot</th>
              <th>Avaiable lot</th>
            </tr>
            <tr v-for="carpark in largeSCP" v-bind:key="carpark.carpark_number">
              <td>{{carpark.id}}</td>
              <td>{{carpark.total_lots}}</td>
              <td>{{carpark.lots_available}}</td>
            </tr>
          </table>
        </div>
          </div></div>

   </div> 
   <div v-else> <h1>Loading...</h1></div>
  </div> 
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Users',
    data() {
      return {
        lastUpdated: '',
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
      async sortCarparks(){
        await axios
        .get('https://api.data.gov.sg/v1/transport/carpark-availability')
        .then(res => {
          this.lastUpdated = res.data.items[0].timestamp;
          this.carparks = res.data.items[0].carpark_data.map((carpark)=>{
            return {
              id: carpark.carpark_number,
              total_lots: parseInt(carpark.carpark_info[0].total_lots),
              lots_available: parseInt(carpark.carpark_info[0].lots_available)
            }
          });
        });
        this.resetData();
        this.carparks.forEach((carpark) => {
          if (carpark.total_lots < 100){
            if (this.smallSCP.length == 0){
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
              };
              if (carpark.lots_available >= this.mediumB){
                if (carpark.lots_available == this.mediumB){
                  //Append
                  this.mediumBCP.push(carpark);
                } else {
                  this.mediumB = carpark.lots_available;
                  this.mediumBCP = [carpark];
                }
              };
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
              };
              if (carpark.lots_available >= this.bigB){
                if (carpark.lots_available == this.bigB){
                  //Append
                  this.bigBCP.push(carpark);
                } else {
                  this.bigB = carpark.lots_available;
                  this.bigBCP = [carpark];
                }
              };
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
              };
              if (carpark.lots_available >= this.largeB){
                if (carpark.lots_available == this.largeB){
                  //Append
                  this.largeBCP.push(carpark);
                } else {
                  this.largeB = carpark.lots_available;
                  this.largeBCP = [carpark];
                }
              };
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

    created: async function() {
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

  .column-4 {
    float: left;
    width: 25%;
  }

  .column-2 {
    float: center;
    width: 100%;
  }

  /* Clear floats after the columns */
  .row:after {
    content: "";
    display: table;
    clear: both;
  }

  table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
  padding: 10px;
}

  table {
    margin-left: auto;
  margin-right: auto;
  }
</style>