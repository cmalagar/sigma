<template>
  <div id="serverCard" :class="cardClassChanger">
    <application
      v-for="application in server.applications"
      v-bind:id="application.id"
      v-bind:title="application.title"></application>
  </div>
</template>

<script type="text/javascript">
  import Application from './Application'

  export default {
    props: ['server'],

    components: {
      Application
    },

    computed: {
      // Determines the color of the server card
      cardClassChanger: function () {
        if (this.server.applications.length === 0) {
          return 'emptyServer'
        } else if (this.server.applications.length === 1) {
          if (this.server.applications[0].id === 'Ch') {
            return 'chronos'
          } else if (this.server.applications[0].id === 'Hd') {
            return 'hadoop'
          } else if (this.server.applications[0].id === 'Rl') {
            return 'rails'
          } else if (this.server.applications[0].id === 'Sp') {
            return 'spark'
          } else if (this.server.applications[0].id === 'St') {
            return 'storm'
          }
        } else if (this.server.applications.length === 2) {
          if (this.server.applications[0].id === 'Ch') {
            if (this.server.applications[1].id === 'Ch') {
              return 'chronos'
            } else if (this.server.applications[1].id === 'Hd') {
              return 'chronosHadoop'
            } else if (this.server.applications[1].id === 'Rl') {
              return 'chronosRails'
            } else if (this.server.applications[1].id === 'Sp') {
              return 'chronosSpark'
            } else if (this.server.applications[1].id === 'St') {
              return 'chronosStorm'
            }
          } else if (this.server.applications[0].id === 'Hd') {
            if (this.server.applications[1].id === 'Ch') {
              return 'chronosHadoop'
            } else if (this.server.applications[1].id === 'Hd') {
              return 'hadoop'
            } else if (this.server.applications[1].id === 'Rl') {
              return 'hadoopRails'
            } else if (this.server.applications[1].id === 'Sp') {
              return 'hadoopSpark'
            } else if (this.server.applications[1].id === 'St') {
              return 'hadoopStorm'
            }
          } else if (this.server.applications[0].id === 'Rl') {
            if (this.server.applications[1].id === 'Ch') {
              return 'chronosRails'
            } else if (this.server.applications[1].id === 'Hd') {
              return 'hadoopRails'
            } else if (this.server.applications[1].id === 'Rl') {
              return 'rails'
            } else if (this.server.applications[1].id === 'Sp') {
              return 'railsSpark'
            } else if (this.server.applications[1].id === 'St') {
              return 'railsStorm'
            }
          } else if (this.server.applications[0].id === 'Sp') {
            if (this.server.applications[1].id === 'Ch') {
              return 'chronosSpark'
            } else if (this.server.applications[1].id === 'Hd') {
              return 'hadoopSpark'
            } else if (this.server.applications[1].id === 'Rl') {
              return 'railsSpark'
            } else if (this.server.applications[1].id === 'Sp') {
              return 'spark'
            } else if (this.server.applications[1].id === 'St') {
              return 'sparkStorm'
            }
          } else if (this.server.applications[0].id === 'St') {
            if (this.server.applications[1].id === 'Ch') {
              return 'chronosStorm'
            } else if (this.server.applications[1].id === 'Hd') {
              return 'hadoopStorm'
            } else if (this.server.applications[1].id === 'Rl') {
              return 'railsStorm'
            } else if (this.server.applications[1].id === 'Sp') {
              return 'sparkStorm'
            } else if (this.server.applications[1].id === 'St') {
              return 'storm'
            }
          }
        } else {
          return 'invalidApplication'
        }
      }
    }
  }
</script>

<style>
  #serverCard {
    height: 60px;
    width: 90px;
    padding: 20px;
    border: 8px solid #000000;
    border-radius: 15px;
    text-align: center;
  }

  .emptyServer {
    background-color: #282828;
  }

  .chronos {
    background: #66ccff;
  }

  .chronosHadoop {
    background: #66ccff;
    background: -webkit-linear-gradient(#66ccff, #990066);
    background: -o-linear-gradient(#66ccff, #990066);
    background: -moz-linear-gradient(#66ccff, #990066);
    background: linear-gradient(#66ccff, #990066);
  }

  .chronosRails {
    background: #66ccff;
    background: -webkit-linear-gradient(#66ccff, #3333ff);
    background: -o-linear-gradient(#66ccff, #3333ff);
    background: -moz-linear-gradient(#66ccff, #3333ff);
    background: linear-gradient(#66ccff, #3333ff);
  }

  .chronosSpark {
    background: #66ccff;
    background: -webkit-linear-gradient(#66ccff, #33ff33);
    background: -o-linear-gradient(#66ccff, #33ff33);
    background: -moz-linear-gradient(#66ccff, #33ff33);
    background: linear-gradient(#66ccff, #33ff33);
  }

  .chronosStorm {
    background: #66ccff;
    background: -webkit-linear-gradient(#66ccff, #33ffcc);
    background: -o-linear-gradient(#66ccff, #33ffcc);
    background: -moz-linear-gradient(#66ccff, #33ffcc);
    background: linear-gradient(#66ccff, #33ffcc);
  }

  .hadoop {
    background: #990066;
  }

  .hadoopRails {
    background: #990066;
    background: -webkit-linear-gradient(#990066, #3333ff);
    background: -o-linear-gradient(#990066, #3333ff);
    background: -moz-linear-gradient(#990066, #3333ff);
    background: linear-gradient(#990066, #3333ff);
  }

  .hadoopSpark {
    background: #990066;
    background: -webkit-linear-gradient(#990066, #33ff33);
    background: -o-linear-gradient(#990066, #33ff33);
    background: -moz-linear-gradient(#990066, #33ff33);
    background: linear-gradient(#990066, #33ff33);
  }

  .hadoopStorm {
    background: #990066;
    background: -webkit-linear-gradient(#990066, #33ffcc);
    background: -o-linear-gradient(#990066, #33ffcc);
    background: -moz-linear-gradient(#990066, #33ffcc);
    background: linear-gradient(#990066, #33ffcc);
  }

  .rails {
    background: #3333ff;
  }

  .railsSpark {
    background: #3333ff;
    background: -webkit-linear-gradient(#3333ff, #33ff33);
    background: -o-linear-gradient(#3333ff, #33ff33);
    background: -moz-linear-gradient(#3333ff, #33ff33);
    background: linear-gradient(#3333ff, #33ff33);
  }

  .railsStorm {
    background: #3333ff;
    background: -webkit-linear-gradient(#3333ff, #33ffcc);
    background: -o-linear-gradient(#3333ff, #33ffcc);
    background: -moz-linear-gradient(#3333ff, #33ffcc);
    background: linear-gradient(#3333ff, #33ffcc);
  }

  .spark {
    background: #33ff33;
  }

  .sparkStorm {
    background: #33ff33;
    background: -webkit-linear-gradient(#33ff33, #33ffcc);
    background: -o-linear-gradient(#33ff33, #33ffcc);
    background: -moz-linear-gradient(#33ff33, #33ffcc);
    background: linear-gradient(#33ff33, #33ffcc);
  }

  .storm {
    background: #33ffcc;
  }

  .invalidApplication {
    background: #ff0000;
  }
</style>
