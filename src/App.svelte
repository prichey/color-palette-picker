<script>
  import palettes from "./100.json";
  let selectedIds = [];
  const handleRowClick = rowId => {
    if (!selectedIds.includes(rowId)) {
      selectedIds = [...selectedIds, rowId];
    } else {
      selectedIds = selectedIds.filter(id => id !== rowId);
    }
  };

  $: {
    selectedIds = selectedIds.sort((a, b) => a - b);
  }
</script>

<style>
  * {
    box-sizing: border-box;
    position: relative;
  }
  :global(body),
  :global(html) {
    height: 100vh;
    overflow: hidden;
  }

  :global(body) {
    padding: 2em;
    display: flex;
    flex-wrap: nowrap;
    flex-direction: column;
  }

  h1 {
    text-align: center;
  }

  main {
    text-align: center;
    height: 100%;
    padding: 0;
    margin: 0 auto;
    overflow: hidden;
    max-width: 1000px;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
  }

  span {
    font-size: 24px;
  }

  ul {
    list-style: none;
  }

  main > * {
    overflow-y: scroll;
    max-height: 100%;
    padding: 20px;
  }

  li.outer {
    display: flex;
    flex-wrap: none;
    justify-content: center;
    margin-bottom: 25px;
    align-items: center;
  }

  li.inner {
    display: inline-block;
    width: 50px;
    height: 50px;
  }

  .list li.outer {
    cursor: pointer;
  }
</style>

<h1>color picker!</h1>
<main>
  <div class="list">
    <h3>Full list</h3>
    <ul class="outer">
      {#each palettes as palette, i}
        <li class="outer" on:click={() => handleRowClick(i)}>
          <div class="label">
            <span>#{i + 1}</span>
          </div>
          <ul class="inner palette">
            {#each palette as color}
              <li class="inner" style={`background-color: ${color}`} />
            {/each}
          </ul>
        </li>
      {/each}
    </ul>
  </div>

  <div class="selections">
    <h3>Selections</h3>
    <ul>
      {#each selectedIds as id}
        <li class="outer">
          <div class="label">
            <span>#{id + 1}</span>
          </div>
          <ul class="inner palette">
            {#each palettes[id] as color}
              <li class="inner" style={`background-color: ${color}`} />
            {/each}
          </ul>
        </li>
      {/each}
    </ul>
  </div>
</main>
