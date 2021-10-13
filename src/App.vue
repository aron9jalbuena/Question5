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

          <b-form-group
            id = "input-group-2"
            label = "Key"
            label-for = "input-2"
            description = "Key For Text"
          >
            <b-form-input
              id = "input-2"
              v-model="form.key"
              placeholder="Key"
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
        text: '',
        key: ''
      },
      info: '',
      decryptext: '',
      show: true
    }
  },

  methods:{

    displayinfo(){
      axios
        .post('http://localhost:1323/add', {
          text: this.form.text,
          keyinput: this.form.key
        })
        .then(response => {
          this.info = response.data
        })
        .catch(error => console.log(error))
    },

    decryptinfo(){
      axios
        .post('http://localhost:1323/get', {
          cid: this.info,
          keyinput: this.form.key
        })
        .then(response => {
          this.decryptext = response.data
        })
        .catch(error => {
          console.log(error)
        })
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
