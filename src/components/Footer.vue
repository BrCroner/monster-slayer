<template>
  <footer>
    <ul class="hstack gap-5">
      <li>
        <a target="_blank" href="https://twitter.com/BrCroner">
          <img src="@/assets/twitter-logo.svg" alt="Twitter logo" />
        </a>
      </li>
      <li>
        <a target="_blank" href="https://www.instagram.com/brcroner/">
          <img src="@/assets/instagram-logo.svg" alt="Instagram logo" />
        </a>
      </li>
      <li>
        <a
          target="_blank"
          href="https://web.whatsapp.com/send?phone=5561981167309&text&app_absent=0"
        >
          <img src="@/assets/whatsapp-logo.svg" alt="WhatsApp logo" />
        </a>
      </li>
    </ul>
  </footer>
</template>

<style scoped>
img {
  vertical-align: middle;
  width: 30px;
}
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 50px;
  background-color: var(--color-background-nav);
  display: flex;
  justify-content: center;
  align-items: center;
}
footer ul {
  padding-top: 15px;
  display: flex;
  align-items: center;
  list-style: none;
}
</style>
