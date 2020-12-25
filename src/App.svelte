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
    // overflow: hidden;
    /* Hide scrollbar for Chrome, Safari and Opera */
    &::-webkit-scrollbar {
      display: none;
    }

    /* Hide scrollbar for IE, Edge and Firefox */
    &::-webkit-scrollbar {
      -ms-overflow-style: none; /* IE and Edge */
      scrollbar-width: none; /* Firefox */
    }
  }

  main {
    // height: 100vh;
    height: auto;
  }
</style>
