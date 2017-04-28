<template>
  <div id="app">
    <greeting></greeting>
    <DatePicker></DatePicker>
  </div>
</template>

<script>
import Greeting from './components/Greeting'
import DatePicker from './components/DatePicker'

export default {
  name: 'app',
  components: {
    Greeting,
    DatePicker
  }
}
</script>

<style lang="sass">
  html {
    background: url('http://i.imgur.com/DRNFL2C.jpg') no-repeat center center fixed; 
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
  }
  body {
    background: url('http://i.imgur.com/DRNFL2C.jpg') no-repeat center center fixed; 
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
  }
</style>
