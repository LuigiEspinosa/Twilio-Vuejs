<template>
  <div class="chat-container" id="app">
    <aside class="col-md-4 left-nav">
      <h1>Menú izquierda</h1>
    </aside>

    <div class="box-container">
      <div class="header">
        <h1>Header</h1>
      </div>

      <div class="chat-room" v-if="authenticated">
          <Rooms />
          <Logs />
          <Video :username="username" />
      </div>

      <div class="container submit-form" v-else>
        <div class="username">
          <form class="form-inline" @submit.prevent="submitUsername(username)">
            <div class="form-group mb-2">
              <input type="text" class="form-control" v-model="username">
            </div>
            
            <button type="submit" class="btn btn-primary mb-2 Botton">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Rooms from './components/Rooms'
  import Video from './components/Video'
  import Logs from './components/Logs'
  // import AddRoom from './components/AddRoom'

  export default {
    name: 'App',
    
    data() {
      return {
        username: "",
        authenticated: false
      }
    },

    components: {
      Rooms,
      Video,
      Logs,
      // AddRoom
    },

    methods: {
      submitUsername(username) {
        if(!username) {
          return alert('please provide a username');
        }

        this.authenticated = true;
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
    color: #444;
    min-height: 100vh;
    background-color: #fff;
  }

  h1 {
    color: #262044;
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 1rem;
  }

  .left-nav {
    -webkit-box-align: center;
    align-items: center;
    background-color: rgb(255, 255, 255);
    box-shadow: rgba(0, 0, 0, 0.3) 20px 0px 24px -19px;
    color: rgb(93, 93, 93);
    display: flex;
    flex-flow: column nowrap;
    height: calc(100vh + 2rem);
    justify-content: space-evenly;
    left: 0px;
    margin: -1rem 0px;
    position: fixed;
    top: 0px;
    width: 24rem;
    z-index: 9999;
  }

  .box-container {
    background-color: rgb(255, 255, 255);
    margin-left: 24rem;
    min-height: 100vh;
  }

  .header,
  .submit-form {
    -webkit-box-align: center;
    align-items: center;
    display: flex;
    flex-flow: row nowrap;
    -webkit-box-pack: justify;
    justify-content: center;
    margin: 2rem auto;
    padding: 1rem;
    width: 100%;
    height: 4rem;
  }

  .header { 
    box-shadow: rgba(0, 0, 0, 0.3) 20px 0px 24px -19px;
  }

  .chat-room {
    box-shadow: rgba(0, 0, 0, 0.3) 20px 0px 24px -19px;
    padding: 0;
    max-width: 100%;
    -webkit-box-align: center;
    align-items: center;
    display: flex;
    flex-flow: column nowrap;
    -webkit-box-pack: justify;
    justify-content: space-evenly;
  }

  .box {
    border: 1px solid #808080;
  }

  .username {
    margin: 12px auto 7px auto;
    color: #444;
  }

  .Botton {
    color: #fff;
    background-color: #4d555f;
    border-color: #303840;
    padding: 8px;
    font-weight: bolder;
  }
</style>
