<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <nav>
      <div class="logo">
        <img src="./assets/logo.svg" alt="logo" />
      </div>
      <div class="menu">
        <img src="./assets/menu.svg" alt="menu" />
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
      </div>
    </nav>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
  <footer>
    <p>Footer</p>
  </footer>

</template>
<script>
export default {
  // create method to connect websocket
  created() {
    this.connect();
  },
  methods: {
    connect() {
      // connect to websocket
      const socket = new WebSocket("ws://localhost:8080");

      // listen to websocket events
      socket.addEventListener("open", () => {
        console.log("connected to server");
      });

      socket.addEventListener("message", (message) => {
        console.log("received message", message.data);
      });

      socket.addEventListener("close", () => {
        console.log("disconnected from server");
      });
    },
  },
};
}
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
