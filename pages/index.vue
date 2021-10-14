<template>
  <div class="App">
    <div class="right-section">
      <div class="welcoming">HELLO</div>
      <div class="welcome-name">{{message.name}}</div>
      <iframe width="100%" height="100" src="http://localhost:5500" title="form-name" frameborder="0"
        @load="getMessage"></iframe>
    </div>
    <div class="left-section">
      <img src="~assets/logo.png" alt="logo" width="100%">
      <div class="thank-word">
        <div class="thanks-to">
          Thank to
        </div>
        <div class="name">{{message.name}}</div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        message: {
          name: ''
        }
      }
    },
    beforeDestroy() {
      window.removeEventListener('message', this.receiveMessage)
    },
    methods: {
      getMessage() {
        window.addEventListener('message', this.receiveMessage)
      },
      receiveMessage(event) {        
        if (event.origin !== 'http://localhost:5500') return
        console.log(event)
        try {
          let messageData = JSON.parse(event.data)
          if (messageData.event !== 'message_name') return
          this.message.name = messageData.message
        } catch {
        }
      }
    },
  }

</script>

<style scoped>
  .App {
    display: grid;
    grid-template-columns: 60% 40%;
    width: 100vw;
    height: 100vh;
  }

  .right-section {
    background: linear-gradient(90deg, rgba(255, 255, 255, 1) 47%, rgba(217, 94, 124, 0.3127626050420168) 76%);
    text-align: center;
    position: relative;
  }

  .welcoming {
    font-family: 'Poppins', sans-serif;
    font-size: 9rem;
    font-weight: bold;
    color: #999;
    letter-spacing: 20px;
    margin-top: 4rem;
  }

  .welcome-name {
    color: #e14c81;
    font-family: 'Sacramento', cursive;
    font-weight: bold;
    font-size: 8rem;
    position: absolute;
    top: 10rem;
    line-height: 0.8;
    text-transform: lowercase;
  }

  .left-section {
    padding: 2rem;
    font-family: 'Poppins', sans-serif;
    position: relative;
  }

  .thanks-to {
    transform: rotate(-90deg);
    width: 70px;
    font-size: 16px;
  }

  .thanks-to::after {
    content: '';
    width: 78px;
    height: 2px;
    position: absolute;
    bottom: -9px;
    left: 0px;
    /* top: 0; */
    background: black;
  }

  .name {
    text-transform: uppercase;
    font-size: 20px;
  }

  .thank-word {
    display: flex;
    align-items: center;
    position: absolute;
    bottom: 8rem;
  }

  iframe {
    margin-top: 10rem;
  }

</style>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Poppins&family=Sacramento&display=swap');

  body {
    margin: 0;
  }

  * {
    box-sizing: border-box;
  }

</style>
