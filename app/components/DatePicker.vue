<template>
  <div class="datepicker">
      <h1>{{date}}</h1>
  </div>
</template>

<script>
export default {
  name: 'datepicker',
 data () {
    return {
      date: 'Welcome to My Vue App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>
h1 {
    text-align: center;
    font-size: 32px;
    color: white;
    text-shadow: 2px 2px black;
    margin-top: 80px;
}
</style>