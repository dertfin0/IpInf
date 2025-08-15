<script setup></script>

<template>
  <div className="container">
    <h1>Get IP Info</h1>
    <div id="main" v-if="isMainState">
      <p>Get address Country, City and Provider at 2 clicks!</p>
      <input v-model="ipAddress" placeholder="Enter IP address" maxlength="39"></input><br/>
      <button :class="{nonActiveButton: ipAddress == ''}">Get {{ buttonAddressPlaceholder }} info</button>
    </div>
  </div>
  <p class="author">by dertfin1</p>
</template>

<script>
export default {
  data() {
    return {
      ipAddress: "3d67:49a7:e0c4:c4e9:9d0e:a3d4:5d61:d263",
      isMainState: false
    }
  },
  computed: {
    buttonAddressPlaceholder() {
      if (this.ipAddress == "") return "address";
      return this.ipAddress.length <= 15 ? this.ipAddress : "address"; // IPv4 будет отображаться в кнопке, а IPv6 - нет, тк длинный
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
</style>
