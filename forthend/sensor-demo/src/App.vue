<script>
import axios from 'axios'
 export default{
  data(){
    return{
      sensors:[
        {id:1,name:"温度传感器"}

      ]
    }
  },
  mounted(){
    this.getSensors()
  },
  methods:{
    async getSensors(){
      const res = await axios.get('https://nora647-redesigned-space-spoon-4rq6rr6j5v4h57jv-8080.preview.app.github.dev/api/sensors')
      this.sensors = res.data;    
    },
    async deleteSensor(sensor){
       const res = await axios.delete('https://nora647-redesigned-space-spoon-4rq6rr6j5v4h57jv-8080.preview.app.github.dev/api/sensors/'+sensor.id)
        this.getSensors();
      },
      async addOneSensor(){
        await axios.post('https://nora647-redesigned-space-spoon-4rq6rr6j5v4h57jv-8080.preview.app.github.dev/api/sensors/',
        {
          name: "NewSensor"
        })
        this.getSensors();
      }
    }
  }
</script>

<template>
  <button @click="getSensors">Get all sensors</button>
  <button @click="addOneSensor">Add One Sensor</button>
<ul>
  <li v-for="sensor in sensors" key="sensor.id">
    {{sensor.id}}-{{sensor.name}}
    <button @click="deleteSensor(sensor)">x</button>
  </li>
</ul>
</template>

<style scoped>

</style>
