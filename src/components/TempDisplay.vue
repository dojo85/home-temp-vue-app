<template>
<div v-if="sensordata == null" class="row justify-content-center m-5 p-5">
                <div class="spinner-grow text-primary m-1" role="status">
                    <span class="visually-hidden">Loading...</span>
                  </div>
                  <div class="spinner-grow text-primary m-1" role="status">
                    <span class="visually-hidden">Loading...</span>
                  </div>
                  <div class="spinner-grow text-primary m-1" role="status">
                    <span class="visually-hidden">Loading...</span>
                  </div>
</div>
<div v-else class="row justify-content-center text-center">

    <div class="d-flex flex-column temp-box justify-content-center align-tems-between bg-primary text-light">
        <div class="fw-light">
            <i class="bi bi-clock" style="font-size: 0.9rem;"></i>
            {{ getDateTime(sensordata.dateTime) }} 
        </div> 
        <div class="temp-text">
            {{ sensordata.temperature }}°C
        </div> 
        <div class="fw-light">
            <i class="bi bi-moisture"></i> Hum.: {{sensordata.humidity}}%
        </div>
    </div>
</div>
</template>

<script>
export default {
props: ['sensordata'],
    methods: {
        getDate: function(date) {
          let convertedDate = new Date(date);   
          return this.ddMMyyyy(convertedDate);          
        },
        getTime: function(date) {
          let convertedDate = new Date(date);   
          return this.HHmm(convertedDate);
        },
        getDateTime(date) {
          let newDate = new Date(date);
          return this.ddMMyyyy(newDate)+' '+this.HHmm(newDate);
        },
        ddMMyyyy: function (date){
          let dd = date.getDate();
          let MM = date.getMonth() + 1;
          let yyyy = date.getFullYear();
          
          dd = dd>9 ? dd : '0' + dd;
          MM = MM>9 ? MM : '0' + MM;
          
          return dd+'.'+MM+'.'+yyyy;
        },        
        HHmm: function (date) {
          let HH = date.getHours();
          let mm = date.getMinutes();
          
          HH = HH>9 ? HH : '0' + HH;
          mm = mm>9 ? mm : '0' + mm;
          
          return HH+':'+mm;
        }  
    }
}
</script>

<style>
.temp-text {
    display: block;
    font-size: 5rem;
    font-weight: 600;    
}

.temp-box {
    position: relative;
    height: 12rem !important;
    width: fit-content !important;
    border: solid 2px rgb(37, 136, 230);
    border-radius: 8px;
    margin: 8px;
    padding: 1rem 1rem;
}

.refresher {
    position: absolute;
    right: 0;
    bottom: 0;
    font-size: 1.5rem;  
    font-weight: 800; 
}
</style>