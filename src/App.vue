<template>
  <div id="app">
    <div class="control-content">
      <server-control-panel
        v-on:add-chronos-instance="addChronosInstance"
        v-on:add-hadoop-instance="addHadoopInstance"
        v-on:add-rails-instance="addRailsInstance"
        v-on:add-server="addServer"
        v-on:add-spark-instance="addSparkInstance"
        v-on:add-storm-instance="addStormInstance"
        v-on:delete-server="deleteServer"
        v-on:delete-chronos-instance="deleteChronosInstance"
        v-on:delete-hadoop-instance="deleteHadoopInstance"
        v-on:delete-rails-instance="deleteRailsInstance"
        v-on:delete-spark-instance="deleteSparkInstance"
        v-on:delete-storm-instance="deleteStormInstance"></server-control-panel>
    </div>
    <div class="canvas-content">
      <h3>Server Canvas</h3>
      <server-canvas v-bind:servers="servers"></server-canvas>
    </div>
  </div>
</template>

<script type="text/javascript">
  import ServerCanvas from './components/ServerCanvas'
  import ServerControlPanel from './components/ServerControlPanel'

  export default {
    name: 'app',

    components: {
      ServerCanvas,
      ServerControlPanel
    },

    data () {
      return {
        servers: [{
          applications: []
        }, {
          applications: []
        }, {
          applications: []
        }, {
          applications: []
        }]
      }
    },

    methods: {
      // Adds server directly to the servers in the component
      addServer: function () {
        this.servers.push({
          isFull: false,
          applications: []
        })
      },

      // Removes server directly from the saved servers from this component
      deleteServer: function () {
        if (this.servers.length !== 0) {
          let applications = this.servers[this.servers.length - 1].applications
          let self = this

          // If server to be deleted contains applications, then add those
          // applications to other servers in the cluster if available
          if (applications.length !== 0) {
            applications.forEach(function (element) {
              if (element.id === 'Ch') {
                self.addChronosInstance()
              } else if (element.id === 'Hd') {
                self.addHadoopInstance()
              } else if (element.id === 'Rl') {
                self.addRailsInstance()
              } else if (element.id === 'Sp') {
                self.addSparkInstance()
              } else if (element.id === 'St') {
                self.addStormInstance()
              }
            })
          }
          this.servers.pop()
        } else {
          console.log('No servers to delete')
        }
      },

      // Adds an instance of an application to the next available server
      addInstance: function (id, title) {
        // Checks if any server has zero applications running on it
        let server = this.servers.find(function (element) {
          return element.applications.length === 0
        })

        // Checks if any server has only one application running on it
        // if none have zero
        if (server === undefined) {
          server = this.servers.find(function (element) {
            return element.applications.length === 1
          })
        }

        // Adds Chronos application to the appropriate server
        if (server !== undefined) {
          server.applications.push({
            title: title,
            id: id,
            dateAdded: new Date().getTime()
          })
        } else {
          console.log('Servers are full')
        }
      },

      // Adds Chronos instance to the next available server
      addChronosInstance: function () {
        this.addInstance('Ch', 'Chronos')
      },

      // Adds Hadoop instance to the next available server
      addHadoopInstance: function () {
        this.addInstance('Hd', 'Hadoop')
      },

      // Adds Rails instance to the next available server
      addRailsInstance: function () {
        this.addInstance('Rl', 'Rails')
      },

      // Adds Spark instance to the next available server
      addSparkInstance: function () {
        this.addInstance('Sp', 'Spark')
      },

      // Adds Storm instance to the next available server
      addStormInstance: function () {
        this.addInstance('St', 'Storm')
      },

      // Removes the most recent instance of an application in the cluster
      deleteInstance: function (id) {
        // Check if servers that contain two applications are available
        let availServers = this.servers.filter(function (element) {
          return element.applications.length > 1
        })

        // If available, filter only 2nd layer applications
        // If instance found, then delete most recent instance from cluster
        if (availServers.length !== 0) {
          let server = availServers.reverse().find(function (element) {
            return element.applications[1].id === id
          })

          if (server !== undefined) {
            server.applications.pop()
          } else {
            availServers = this.servers.filter(function (element) {
              return element.applications.length > 0
            })

            if (availServers.length !== 0) {
              let server = availServers.reverse().find(function (element) {
                return element.applications[0].id === id
              })

              if (server !== undefined) {
                server.applications.shift()
              } else {
                console.log('No instance found in cluster')
              }
            } else {
              console.log('No instance found in cluster')
            }
          }
        } else {
          // Checks applications running on 1st layer and removes if found
          availServers = this.servers.filter(function (element) {
            return element.applications.length > 0
          })

          if (availServers.length !== 0) {
            let server = availServers.reverse().find(function (element) {
              return element.applications[0].id === id
            })

            if (server !== undefined) {
              server.applications.shift()
            } else {
              console.log('No instance found in cluster')
            }
          } else {
            console.log('No instance found in cluster')
          }
        }
      },

      // Removes most recently added instance of Chronos from the cluster
      deleteChronosInstance: function () {
        this.deleteInstance('Ch')
      },

      // Removes most recently added instance of Hadoop from the cluster
      deleteHadoopInstance: function () {
        this.deleteInstance('Hd')
      },

      // Removes most recently added instance of Rails from the cluster
      deleteRailsInstance: function () {
        this.deleteInstance('Rl')
      },

      // Removes most recently added instance of Spark from the cluster
      deleteSparkInstance: function () {
        this.deleteInstance('Sp')
      },

      // Removes most recently added instance of Storm from the cluster
      deleteStormInstance: function () {
        this.deleteInstance('St')
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    color: #ffffff;
    display: -webkit-flow;
    display: flex;
    -webkit-flex-direction: row;
    flex-direction: row;
  }
</style>
