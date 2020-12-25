<script>
  export let panel;

  let panelType;
  console.log(panel.content.length);

  switch (panel.content.length) {
    case 1:
      panelType = "default";
      break;
    case 2:
      panelType = "split";
      break;
    case 6:
      panelType = "grid";
      break;
    default:
      panelType = "default";
      break;
  }
</script>

<div class="panel">
  <ul class={`panel-content ${panelType}`}>
    {#each panel.content as content}
      <li>{content.altText}</li>
    {/each}
  </ul>
</div>

<style lang="scss">
  .panel {
    height: 100%;
    width: 100%;
    // border: 5px solid black;

    ul {
      height: 100%;
      list-style: none;
      padding: 0;
      margin: 0;
      grid-gap: 10px;

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
        height: 100%;
        width: 100%;
        border: 5px solid black;
      }
    }
  }
</style>
