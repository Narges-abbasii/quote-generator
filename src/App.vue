<script setup>
import Quote from "./components/Quote.vue";
</script>

<template>
  <Quote />

  <footer class="attribution">
    <p>
      This project was coded by
      <a href="https://github.com/Narges-abbasii" target="_blank"
        >Narges Abbasi</a
      >
      and is open-source on
      <a
        href="https://github.com/Narges-abbasii/quote-generator"
        target="_blank"
        >GitHub</a
      >.
    </p>
  </footer>
</template>

<style scoped>
.attribution {
  font-size: 14px;
  position: fixed;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  color: white; /* soft dark gray text */
  background: var(--color-Dark-Grayish-Blue); /* very light gray background */
  padding: 10px 18px;
  border-radius: 10px;

  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05); /* very light soft shadow */
}

.attribution p {
  margin: 0;
}

.attribution a {
  color: var(--color-neon-green); /* fresh soft green */
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s;
}

.attribution a:hover {
  text-decoration: underline;
}

@media screen and (max-width: 480px) {
  .attribution {
    font-size: 12px;
    padding: 8px 14px;
  }
}
</style>
