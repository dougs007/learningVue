<template>
  <div id="app">
    <h1>Problem of Monty|Hall</h1>
    <button class="button-reset" @click="resetApp">Reset</button>
    <div class="form">
      <div v-if="!started">
        <label for="portsAmount">How much door(s) ?</label>
        <input type="text" id="portsAmount" size="3"
          v-model.number="portsAmount"
        >
        <div v-if="!started">
          <label for="selectedPort">Wich door is the winner ?</label>
          <input type="text" id="selectedPort" size="3"
            v-model.number="selectedPort"
          >
        </div>
        <button v-if="!started" @click="startApp">Start</button>
        <button v-if="started" @click="started = false">Reset</button>
      </div>
      <div class="doors" v-if="started">
        <div v-for="port in portsAmount" :key="port" >
          <Door :number="port" :hasGift="port === selectedPort" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Door from './components/Door';

export default {
  name: 'App',
  components: { Door },
  data: function() {
    return {
      started: false,
      portsAmount: 3,
      selectedPort: null,
    }
  },
  methods: {
    startApp() {
      if (this.portsAmount < this.selectedPort) {
        alert('Please, the winner door must be in the number of doors existents !')
        return;
      }
      this.started = true;
      console.log('app has started!!');
    },
    resetApp() {
      this.started = false;
      this.portsAmount = 3;
    }
  }
}
</script>

<style>

  * {
    box-sizing: border-box;
    font-family: 'Montserrat', sans-serif;
  }

  body {
    color: #FFF;
    background: linear-gradient(to right, rgb(21, 153, 87), rgb(21, 87, 153));
  }

  #app {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  #app h1 {
    border: 1px solid #000;
    background-color: #0004;
    padding: 20px;
    margin-bottom: 30px;
  }

  .form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 40px;
  }

  .form, .form input, .form button {
    margin-bottom: 10px;
    font-size: 2rem;
  }

  .doors {
    align-self: stretch;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
  }

  .button-reset {
    margin: 0px 0px 30px 0px;
  }

</style>
