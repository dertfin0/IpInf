<script setup></script>

<template>
  <div className="container">
    <h1>Get IP Info</h1>
    <div id="main" v-if="isMainState">
      <p>Get address Country, City and Provider at 2 clicks!</p>
      <input v-model="ipAddress" placeholder="Enter IP address" maxlength="39"></input><br/>
      <button :class="{nonActiveButton: ipAddress == ''}" @click="getIpInfo()">Get {{ buttonAddressPlaceholder }} info</button>
      <p class="error" v-show="error != ''">{{ error }}</p>
    </div>

    <div id="info" v-else>
      <p id="subtitle">{{ ipAddress}} information</p>
      <br/>
      <div v-if="ipInfo.country != null">
        <h3>Country</h3>
        <p>{{ ipInfo.country }}</p>
      </div>
      <div v-if="ipInfo.city != null">
        <h3>City</h3>
        <p>{{ ipInfo.city }}</p>
      </div>
      <div v-if="ipInfo.org != null">
        <h3>Provider</h3>
        <p>{{ ipInfo.org }}</p>
      </div>
      <div class="go-back" @click="isMainState = true"><h5><</h5></div>
    </div>
  </div>
  <p class="author">by dertfin1</p>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      ipAddress: "",
      isMainState: true,
      error: "",
      ipInfo: {}
    }
  },
  computed: {
    buttonAddressPlaceholder() {
      if (this.ipAddress == "") return "address";
      return this.ipAddress.length <= 15 ? this.ipAddress : "address"; // IPv4 будет отображаться в кнопке, а IPv6 - нет, тк длинный
    }
  },
  methods: {
    getIpInfo() {
      this.error = "";
      if (this.ipAddress == "") {
        this.error = "Enter IP address!";
        return;
      }

      axios.get(`http://ip-api.com/json/${this.ipAddress}`)
        .then(response => {
          if (response.data.status != "success") {
            this.error = "IP address not valid!";
          } else {
            this.ipInfo = response.data;
            this.isMainState = false;
          }
        })
        .catch(error => this.error = "Unknown error!")
    }
  }
}
</script>

<style scoped>
.author {
  position: absolute;
  bottom: 0.5vh;
  right: 0.5vw;
  color: white;
  font-family: "Monserrat";
  margin-bottom: 0;
}
.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  color: white;
  font-family: "Monserrat";
  box-shadow: 0px 0px 10px #1d1d1d;

  background: #242424;
  background: linear-gradient(318deg,rgba(36, 36, 36, 1) 0%, rgba(59, 59, 59, 1) 100%);

  border-radius: 13px;
  padding: 5vh 5vw 5vh 5vw;

  text-align: center;
}

p {
  margin-bottom: 4vh;
}

input {
  padding: 1vh 2vw 1vh 2vw;
  border-radius: 8px;
  display: inline-block;
  margin-bottom: 1vh;
  text-align: center;
  color: white;
  font-family: "Monserrat";

  border: none;

  background: #464646;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.3);

  transition: all .4s;
}

input:hover {
  background: #4b4b4b;
  box-shadow: 0px 0px 5px rgba(255, 255, 255, 0.1);
}

input:focus {
  outline: none;
  background: #525252;
  transition: all 1s;
}

button {
  padding: 0.5vh 2vw 0.5vh 2vw;
  display: inline-block;
  margin-bottom: 0.5vh;

  border: none;
  border-radius: 5px;

  color: white;
  font-family: "Monserrat";

  background: #424242;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.3);

  transition: 0.4s;
}

button:hover {
  box-shadow: 0px 0px 5px rgba(138, 138, 138, 0.1);
}

.nonActiveButton {
  background: #363636;
}

.error {
  color: red;
  font-family: "Monserrat";
  margin-bottom: 0;
  font-size: 0.9em;
}

#info #subtitle {
  margin-bottom: 0;
}

#info h3 {
  font-size: 1.3em;
}

#info p {
  font-size: 1em;
  margin-bottom: 2vh;
}

.go-back {
  color: white;
  font-family: "Monserrat";
  position: absolute;
  padding: 20px;
  bottom: 0;
  left: 0;
}

.go-back:hover {
  cursor: pointer;
}

@media screen and (max-width: 550px) {
  .container {
    width: 70vw;
  }
}

@media screen and (max-width: 360px) {
  .container {
    width: 80vw;
  }
}
</style>
