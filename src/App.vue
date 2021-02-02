<template>
  <div>
    <Dropdown/>
    <ColorPicker/>
  </div>
</template>

<script>
import ColorPicker from './components/ColorPicker'
import Dropdown from './components/Dropdown'
import mqtt from 'mqtt'

export default {
  name: 'app',

  components: {
    ColorPicker,
    Dropdown,
  },

  data: function() {
    return {
      host: "raspberrypi",
      port: 9001,
      clientID: "Website-9F888F",
      mqttClient: null,
      pickerValue: ColorPicker.currHexaColor
    }
  },

  methods: {
    connectMQTT(){
      const connectUrl = `ws://${this.host}:${this.port}`
      try{
        this.mqttClient = mqtt.connect(connectUrl)
      }catch(e){
        console.log('mqtt.connect error', e)
      }
      this.mqttClient.on('connect', () => {
        console.log('Connection succeeded!')
      })
      this.mqttClient.on('error', error => {
        console.log('Connection failed', error)
      })
      this.mqttClient.on('message', (topic, message) => {
        this.receiveNews = this.receiveNews.concat(message)
        console.log(`Received message ${message} from topic ${topic}`)
      })
    },
    pubColor(){
      
    }
  },
  mounted: function(){
    this.connectMQTT()
    console.log(this.pickerValue)
  },
};
</script>
