<template>
  <footer>
      <p>
        Made with ❤️ by
        <a href="https://maeldonn.github.io/" target="_blank">maeldonn</a>
      </p>
    </footer>
</template>

<script>
export default {
  name: 'Footer',
};
</script>

<style scoped>
footer {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  justify-content: center;
  margin: 1rem 0;
}
footer a {
  text-decoration: none;
  color: inherit;
}
</style>
