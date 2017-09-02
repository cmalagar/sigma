<template>
  <div id="serverCanvas">
    <server v-for="server in this.servers" v-bind:server="server"></server>
  </div>
</template>

<script type="text/javascript">
  import Server from './Server'

  export default {
    props: ['servers'],

    components: {
      Server
    }
  }
</script>

<style>
  #serverCanvas {
    display: -webkit-flow;
    display: flex;
    -webkit-flex-flow: row wrap;
    flex-flow: row wrap;
    -webkit-align-content: space-around;
    align-content: space-between;
  }
</style>
