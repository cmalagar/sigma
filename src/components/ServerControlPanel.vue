<template>
  <div id="serverControlPanel">
    <div class="serverContent">
      <h5>
        Add Server
        <input type="button" value="+" v-on:click="addServer"/>
      </h5>
      <h5>
        Delete Server
        <input type="button" value="-" v-on:click="deleteServer"/>
      </h5>
    </div>
    <div class="availableApps">
      <h5>Available Apps</h5>
      <h4>
        Hadoop
        <input type="button" value="-" v-on:click="deleteHadoopInstance"/>
        <input class="hadoopButton" type="button" value="+" v-on:click="addHadoopInstance"/>
      </h4>
      <h4>
        Rails
        <input type="button" value="-" v-on:click="deleteRailsInstance"/>
        <input class="railsButton" type="button" value="+" v-on:click="addRailsInstance"/>
      </h4>
      <h4>
        Chronos
        <input type="button" value="-" v-on:click="deleteChronosInstance"/>
        <input class="chronosButton" type="button" value="+" v-on:click="addChronosInstance"/>
      </h4>
      <h4>
        Storm
        <input type="button" value="-" v-on:click="deleteStormInstance"/>
        <input class="stormButton" type="button" value="+" v-on:click="addStormInstance"/>
      </h4>
      <h4>
        Spark
        <input type="button" value="-" v-on:click="deleteSparkInstance"/>
        <input class="sparkButton" type="button" value="+" v-on:click="addSparkInstance"/>
      </h4>
    </div>
  </div>
</template>

<script type="text/javascript">
  import ServerCanvas from './ServerCanvas'

  export default {
    props: ['server-control-panel'],

    components: {
      ServerCanvas
    },

    // These functions fire events that trigger other function calls handled
    // by the parent component
    methods: {
      addServer: function (event) {
        console.log('addServer')
        this.$emit('add-server', 'add server')
      },

      deleteServer: function (event) {
        console.log('deleteServer')
        this.$emit('delete-server', 'delete server')
      },

      addHadoopInstance: function (event) {
        console.log('addInstance')
        this.$emit('add-hadoop-instance', 'add instance')
      },

      addSparkInstance: function (event) {
        console.log('addInstance')
        this.$emit('add-spark-instance', 'add instance')
      },

      addRailsInstance: function (event) {
        console.log('addInstance')
        this.$emit('add-rails-instance', 'add instance')
      },

      addStormInstance: function (event) {
        console.log('addInstance')
        this.$emit('add-storm-instance', 'add instance')
      },

      addChronosInstance: function (event) {
        console.log('addInstance')
        this.$emit('add-chronos-instance', 'add instance')
      },

      deleteHadoopInstance: function (event) {
        console.log('deleteHadoopInstance')
        this.$emit('delete-hadoop-instance', 'delete instance')
      },

      deleteSparkInstance: function (event) {
        console.log('deleteSparkInstance')
        this.$emit('delete-spark-instance', 'delete instance')
      },

      deleteRailsInstance: function (event) {
        console.log('deleteRailsInstance')
        this.$emit('delete-rails-instance', 'delete instance')
      },

      deleteStormInstance: function (event) {
        console.log('deleteStormInstance')
        this.$emit('delete-storm-instance', 'delete instance')
      },

      deleteChronosInstance: function (event) {
        console.log('deleteChronosInstance')
        this.$emit('delete-chronos-instance', 'delete instance')
      }
    }
  }
</script>

<style>
  #serverControlPanel {
    margin-top: 20px;
    margin-left: 125px;
    width: 200px;
  }

  .availableApps {
    margin-top: 150px;
  }

  input {
    background: #282828;
    color: #ffffff;
    border-radius: 20px;
  }

  .serverContent input {
    font-size: 30px;
  }

  .chronosButton {
    background: #66ccff;
  }

  .hadoopButton {
    background: #990066;
  }

  .railsButton {
    background: #3333ff
  }

  .sparkButton {
    background: #33ff33;
  }

  .stormButton {
    background: #33ffcc;
  }
</style>
