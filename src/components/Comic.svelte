<script>
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";

  import { panelData } from "../data/panelData";
  import Panel from "./Panel.svelte";

  let activePanel = 0;
  let isTransitioning = false;

  onMount(() => {
    document.addEventListener("wheel", (e) => {
      if (isTransitioning) return;
      // TODO: Debounce/throttle
      // Check scroll down or up
      if (e.deltaY > 0) {
        if (activePanel < panelData.length - 1) {
          activePanel++;
        }
      } else if (e.deltaY < 0) {
        if (activePanel > 0) {
          activePanel--;
        }
      } else {
        console.log("How did you get here");
      }
    });
  });
</script>

<section class="comic">
  <div class="panel-wrapper">
    {#each panelData as panel}
      <!-- {#if panel.order === activePanel} -->
      <div
        class="panel-container"
        in:fly={{ y: 2000, duration: 500 }}
        out:fly={{ y: -2000, duration: 500 }}>
        <Panel {panel} />
      </div>
      <!-- {/if} -->
    {/each}
  </div>
</section>

<style lang="scss">
  .comic {
    padding: 10px;
    height: 100%;

    .panel-wrapper {
      height: 100%;
      display: grid;
      grid-gap: 10px;
      // position: relative;

      .panel-container {
        // position: absolute;
        height: 100%;
        width: 100%;
      }
    }
  }
</style>
