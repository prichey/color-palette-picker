<script>
  import palettes from "./500.json";
  let selectionIds = [];
  const updateSelections = () => {
    selectionIds = [...document.getElementsByTagName("input")]
      .filter(el => el.checked)
      .map(el => parseInt(el.id));
    console.log({ selectionIds });
  };
</script>

<style>
  :global(body),
  :global(html),
  main {
    height: 100vh;
    overflow: hidden;
  }

  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    overflow: hidden;
  }

  span {
    font-size: 24px;
  }

  ul {
    list-style: none;
  }

  .list,
  .selections {
    width: 50%;
    float: left;
    position: absolute;
    top: 0;
    overflow-y: scroll;
    height: 100%;
    padding: 20px 0;
  }

  .list {
    left: 0;
  }

  .selections {
    right: 0;
  }

  li.outer {
    display: flex;
    flex-wrap: none;
    justify-content: center;
    margin-bottom: 25px;
  }

  li.inner {
    display: inline-block;
    width: 50px;
    height: 50px;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <div class="list">
    <h3>Full list</h3>
    <ul class="outer">
      {#each palettes as palette, i}
        <li class="outer">
          <div>
            <label for={i}>#{i + 1}</label>
            <input
              type="checkbox"
              id={i}
              name={i}
              on:change={updateSelections} />
          </div>
          <ul class="inner">
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
      {#each selectionIds as id}
        <li class="outer">
          <div>
            <label>#{id + 1}</label>
          </div>
          <ul class="inner">
            {#each palettes[id] as color}
              <li class="inner" style={`background-color: ${color}`} />
            {/each}
          </ul>
        </li>
      {/each}
    </ul>
  </div>
</main>
