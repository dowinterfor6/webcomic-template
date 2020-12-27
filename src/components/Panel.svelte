<script>
  import { onMount } from "svelte";

  export let panel;

  let panelDiv;

  onMount(() => {
    if (panel.content.some((content) => content.type === "dynamic")) {
      let options = {
        threshold: 1.0,
      };

      const intersectionCb = (entries, observer) => {
        entries.forEach((entry) => {
          console.log(entry.intersectionRatio);
          console.log(entry);
        });
      };

      const observer = new IntersectionObserver(intersectionCb, options);

      // TODO: use ref
      const target = panelDiv;
      if (target) {
        observer.observe(target);
      }
    }
  });
</script>

<div class="panel" bind:this={panelDiv}>
  <ul class={`panel-content ${panel.type}`}>
    {#each panel.content as content}
      {#if content.type === 'titleText'}
        <li class="title">{content.title}</li>
      {:else if content.type === 'static'}
        <li
          class="static"
          style={` bottom: ${content.iPos.bottom}; left: ${content.iPos.left};`}>
          <img
            src={content.img}
            alt={content.alt}
            style={`height: ${content.iSize.x}px; width: auto;`} />
        </li>
      {:else if content.type === 'dynamic'}
        <li class="dynamic" style={`top: ${content.iPos.top}`}>
          <img
            src={content.img}
            alt={content.alt}
            style={`height: ${content.iSize.x}px; width: auto`} />
        </li>
      {:else}
        <li class="default"><img src={content.img} alt={content.alt} /></li>
      {/if}
    {/each}
  </ul>
</div>

<style lang="scss">
  .panel {
    margin: 0 auto;
    // Must be % for intersection observer to remain consistent across screens
    // height: 700px;
    height: 100%;
    width: 461px;

    .panel-content {
      height: 100%;
      list-style: none;
      padding: 0;
      margin: 0;
      grid-gap: 10px;
      position: relative;

      &.default {
        display: flex;
        justify-content: center;
        align-items: center;
      }

      &.split {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
      }

      &.grid {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(2, 1fr);
      }

      li {
        display: flex;
        justify-content: center;
        align-items: center;

        &.default {
          height: 100%;
          width: 100%;
          border: 5px solid black;
        }

        &.title {
          position: absolute;
          color: white;
          font-size: 48px;
          font-family: "Brush Script MT", cursive;
          z-index: 5;
        }

        &.static {
          position: absolute;
        }

        &.dynamic {
          position: absolute;
        }

        img {
          height: 100%;
          width: 100%;
          object-fit: cover;
        }
      }
    }
  }
</style>
