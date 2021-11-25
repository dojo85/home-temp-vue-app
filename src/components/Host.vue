<template>
  <div class="container">
      
      <temp-display :sensordata="sensorRecord" @click="refreshAll" class="refresh"/>
  </div>
</template>

<script>
import TempDisplay from './TempDisplay.vue'

let mockData = [
    {
        id: "jdfjdfjdjf",
        dateTime: "2021-10-27T15:05:00",
        temperature: 15,
        humidity: 53
    },
    {
        id: "jdfjdfjdjf",
        dateTime: "2021-10-27T15:04:00",
        temperature: 21,
        humidity: 53
    },
    {
        id: "jdfjdfjdjf",
        dateTime: "2021-10-27T15:03:00",
        temperature: 21,
        humidity: 53
    },
    {
        id: "jdfjdfjdjf",
        dateTime: "2021-10-27T15:02:00",
        temperature: 21,
        humidity: 53
    },
    {
        id: "jdfjdfjdjf",
        dateTime: "2021-10-27T15:01:00",
        temperature: 21,
        humidity: 53
    }
]

export default {
name: 'Host',
data () {
    return {
              
        // sensorRecord: {
        // id: "abc",
        // dateTime: "2021-10-27T15:05:00",
        // temperature: 0,
        // humidity: 100
        // },
        sensorRecord: null,
        apiUrl: 'https://hometempapi.azurewebsites.net',
        sensorDataList: {}
    }
},
async created(){
    await this.refreshAll()    
},
methods: {
    getDataFromApi: function (url){
        let result = axios.get(this.apiUrl + url)
            .then(response => {
                console.log(response.status)
                return response.data
            })
            .catch(function(error){
                console.log(error)
                return null
            })
        return result
    },
    refreshAll: async function () {
            let url = '/values?last=10';
            let data = await this.getDataFromApi(url);
            console.log(data)
            this.sensorDataList = data;
            this.sensorRecord = this.sensorDataList[0]
        }

},
components: {
    TempDisplay
}
}
</script>

<style>
.refresh:hover {
    cursor: pointer;
}
</style>