<script>
  import Comic from "./components/Comic.svelte";
</script>

<main>
  <Comic />
</main>

<style lang="scss">
  :global(*) {
    box-sizing: border-box;
  }

  :global(body) {
    padding: 0;
    overflow: hidden;
  }

  main {
    height: 100vh;
  }
</style>
