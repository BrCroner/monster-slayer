<template>
  <header>
    <nav>
      <router-link to="/">
        <img src="@/assets/croner-logo.svg" alt="Croner-logo" id="logo" />
      </router-link>

      <img
        @click="toggleMenu"
        src="@/assets/menu.svg"
        alt="Abrir menu"
        id="menu-button"
      />

      <div @click="toggleMenu" id="menu-overlay" v-if="menuAreVisible"></div>

      <div id="menu-items" :class="{ active: menuAreVisible }">
        <img src="@/assets/croner-logo.svg" alt="Croner-logo" id="menu-logo" />

        <ul>
          <li>
            <router-link to="/">Página Inicial</router-link>
          </li>
          <li>
            <router-link to="/MonsterSlayer">Monster Slayer</router-link>
          </li>
          <li>
            <a target="_blank" href="https://github.com/BrCroner"
              >GitHub</a
            >
          </li>
          <li>
            <a
              target="_blank"
              href="https://drive.google.com/file/d/1F4t7Ay2lsJJBs701aV6gXFl-i2VjbC7e/view?usp=sharingf"
              >Curriculum</a
            >
          </li>
          <li>
            <a target="_blank" href="mailto:bruno.croner@outlook.com">Contato</a>
          </li>
        </ul>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return {
      menuAreVisible: false,
    };
  },
  methods: {
    toggleMenu() {
      this.menuAreVisible = !this.menuAreVisible;
    },
  },
};
</script>

<style scoped>
header {
  background-color: var(--color-background-nav);
  height: 70px;
  width: 100%;
}
nav {
  padding: 0 5%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 70px;
}
#logo {
  width: 120px;
}
#menu-button {
  width: 30px;
}
#menu-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 40%;
  height: 100vh;
  background-color: #000;
  opacity: 0.9;
}
#menu-logo {
  width: 120px;
  margin: 40px auto 20px auto;
  display: block;
}
#menu-items {
  position: fixed;
  top: 0;
  right: 0;
  background-color: var(--color-background-nav);
  width: 60%;
  height: 100vh;
  display: none;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  font-size: 1rem;
}
#menu-items.active {
  display: flex;
}
ul {
  vertical-align: middle;
  align-content: center;
  text-align: center;
  list-style: none;
}
ul li {
  margin: 25px 0 0 -25px;
  align-items: center;
}
ul li a {
  font-family: 'Play', sans-serif;
  color: var(--color-text-light);
}

@media (min-width: 700px) {
  #menu-button,
  #menu-logo,
  #menu-overlay {
    display: none;
  }
  #logo {
    width: 120px;
  }
  #menu-items {
    position: static;
    height: 70px;
    width: auto;
    display: flex;
    text-align: center;
  }
  ul {
    display: flex;
    height: 70px;
    align-items: center;
  }
  ul li {
    margin: 0;
    margin-left: 20px;
  }
}
</style>
