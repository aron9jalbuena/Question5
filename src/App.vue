<template>
  <div>
    <b-row>
      <b-col>
        <b-form>
          <b-form-group
            id = "input-group-1"
            label = "Text"
            label-for = "input-1"
            description = "Text To Send To IPFS"
          >
            <b-form-input
              id = "input-1"
              v-model="form.text"
              placeholder="text to send"
              required
            ></b-form-input>
          </b-form-group>
        </b-form>
        <b-button @click="displayinfo()">Send To IPFS</b-button>
        <br>
        <br><b-button @click="decryptinfo()">Decrypt Data</b-button>
      </b-col>

      <b-col>
        Encrypted Data
        <br> {{info}}
      </b-col> 

      <b-col>
        Decrypted Data 
        <br> {{decryptext}}
      </b-col>
    </b-row>
    </div>
</template>

<script>
import axios from 'axios';
export default {
  data () {
    return {
      form:{
        text: ''
      },
      info: '',
      decryptext: '',
      show: true
    }
  },

  methods:{

    onSubmit(){
      alert(this.form.text)
    },

    async displayinfo(){
      var bodyformData = new FormData()
      bodyformData.append('text', this.form.text)
      const inforeturn = await axios.post('http://localhost:1323/add', bodyformData)
      this.info = inforeturn.data
      console.log(this.info)
      console.log(inforeturn.error)
    },

    async decryptinfo(){
      const decrypteddata = await axios.get('http://localhost:1323/get/'+this.info)
      this.decryptext = decrypteddata.data
      console.log(decrypteddata.error)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
