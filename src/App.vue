<template>
  <v-app>
    <Dropdown @host-change="(mac) => onClientChange(mac)"/>
    <p>Selected Macaddress: {{ selectedClient }}</p>
    <ColorPicker @color-change="(hexa) => onHexaColorChange(hexa)"/>
  </v-app>
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

  data: () => {
    return {
      host: "raspberrypi",
      port: 9001,
      clientID: "Website-9F888F",
      mqttClient: null,
      selectedClient: "E0:98:06:86:3A:47"
    }
  },

  methods: {
    connectMQTT(){
      const connectUrl = `mqtt://${this.host}:${this.port}`
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
    onHexaColorChange(val){
      this.pubColor(val)
    },
    onClientChange(val){
      this.selectedClient = val
    },
    pubColor(color){
      color = color.replace("#", "")

      this.mqttClient.publish("led/client/" + this.selectedClient, "all;static;" + color.slice(0, 6))
    }
  },

  mounted: function(){
    this.connectMQTT()
  },
};
</script>