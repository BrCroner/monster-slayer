<template>
  <main>
    <div class="container">
      <div class="row">
        <h2 class="title-home">Monster Slayer</h2>
        <p class="text-top">Página desenvolvida com VUE.js</p>
        <div class="logos">
          <img
            class="logo-vue"
            src="@/assets/vue.js-logo.svg"
            alt="VUE.js logo"
          />
        </div>
        <p class="text-bottom">
          Por meio de um arquivo JSON simulei o uso de um Banco de Dados com
          requisições do tipo <strong>GET</strong> e <strong>POST</strong>. Esse
          exercício faz uso dos pacotes <strong>axios</strong>,
          <strong>json-server</strong> e <strong>vue-router</strong>.
        </p>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  text-align: center;
  background-color: var(--color-background-main);
  justify-content: center;
  align-items: center;
}
main p {
  color: var(--color-text-light);
}
.title-home {
  color: var(--color-text-light);
}
.logos {
  width: 90%;
  display: flex;
  justify-content: center;
  margin: auto;
}
.logos img {
  width: 7rem;
}
.logo-vue {
  display: flex;
  align-items: center;
  justify-content: center;
}
.text-top,
.text-bottom {
  margin: 2rem 0 2rem 0;
}
.text-top {
  font-size: 1.3rem;
}
.text-bottom {
  font-size: 1rem;
  line-height: 1.8rem;
}
@media (min-width: 700px) {
  .title-home {
    font-size: 3.5rem;
  }
  .text-top {
    font-size: 2.5rem;
  }
  .text-bottom {
    font-size: 1.6rem;
    line-height: 2.8rem;
  }
  .logos {
    justify-content: center;
  }

  .logos img {
    margin: 4rem 3rem;
    width: 12rem;
  }
}
</style>
