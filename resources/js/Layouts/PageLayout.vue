<script>
export default {
  data() {
    return {
      isPlaying: false
    }
  },
  methods: {
    setPlaying(mode) {
      this.isPlaying = mode;
      console.log('test');
    }
  },
}
</script>

<template>
  <header>
    <div class="logo">
      <a href="#">
        <img src="/img/logo_temp.png" alt="Test">
      </a>
    </div>
    <nav>
      <a href="/">Play</a>
      <a href="/leaderboard">Leaderboard</a>
      <a href="/about">About</a>
      <a href="/profile">Profile</a>
    </nav>
  </header>

  <slot @gameStart="setPlaying(true)" />

  <footer v-if="!isPlaying">
    <div class="footer-container">
      <span>© 2023 Spoicy</span>
      <span>Powered by <a href="https://vuejs.org/">Vue.js</a></span>
    </div>
  </footer>
</template>

<style>
  #app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    overflow: hidden;
  }
  body {
    background-color: #0C4982;
    font-family: Montserrat, sans-serif;
    font-size: 15px;
  }
  h1, h2, h3, h4, h5, h6, a, label, span {
    font-family: Montserrat, sans-serif;
  }
  h1, h2, h3, h4 {
    font-weight: 700;
  }
  header,
  main,
  footer {
    color: white;
  }

  header,
  .footer-container {
    display: flex;
    justify-content: space-between;
  }

  header {
    padding: 2rem 1.5rem;
    background-color: #0A3B6C;
    width: 100%;
    max-height: 100px;
  }

  header img {
    height: 100%;
  }

  /* Bad fix, revisit if becomes an issue, logo changes or mobile view is worked on */
  header .logo {
    width: 300px;
  }

  main {
    flex: 1;
  }

  footer {
    background-color: #0A3B6C;
    width: 100%;
    font-size: 1.25rem;
    font-weight: 500;
    padding: 0.5rem 1.5rem;
    flex: none;
  }

  .footer-container :last-child {
    text-align: right;
  }

  h1 {
    text-align: center;
    margin-top: 2rem;
    font-size: 3rem;
  }

  a {
    color: white;
    text-decoration: none;
    transition: all 0.5s;
  }

  nav {
    display: flex;
    align-items: center;
  }

  nav a {
    font-weight: 600;
    margin: 0 0.5rem;
    font-size: 1.5rem;
  }

  a:hover,
  a:focus {
    color: #6efaa0;
  }

  .bi {
    color: #6efaa0;
  }

  button.green-accent {
    background-color: #54bf7a;
    color: white;
    border: none;
    cursor: pointer;
    transition: all 0.5s;
  }

  button.green-accent:hover,
  button.green-accent:focus {
    background-color: hsl(141, 46%, 44%);
  }
</style>
