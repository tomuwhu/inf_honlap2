<script>
  var sm = $state(1)
  import Elerh from './lib/elerh.svelte';
  import Oktatas from './lib/oktatas.svelte';
  import Kutatas from './lib/kutatas.svelte';
  import Cv from './lib/csv.svelte';
</script>

<div class="ui pointing menu">
  <button class="{sm == 1 ? 'active' :''} item"
    onclick={() => sm = 1}>
    Adatlap
  </button>
  <button class="{sm == 2 ? 'active' :''} item"
    onclick={() => sm = 2}>
    Oktatás
  </button>
  <button class="{sm == 3 ? 'active' :''} item"
    onclick={() => sm = 3}>
    Kutatás
  </button>
  <button class="{sm == 4 ? 'active' :''} item"
    onclick={() => sm = 4}>
    Szakmai önéletrajz
  </button>
  <div class="right menu">
    <div class="item">
      <div class="ui transparent icon input">
        <input type="text" placeholder="Keresés...">
        <i class="search link icon"></i>
      </div>
    </div>
  </div>
</div>

{#if sm == 1}
  <p><Elerh /></p>
{/if}

{#if sm == 2}
  <p><Oktatas /></p>
{/if}

{#if sm == 3}
  <p><Kutatas /></p>
{/if}

{#if sm == 4}
  <p><Cv /></p>
{/if}

<style>
  button {
    all: unset;
    cursor: pointer;
  }
  button.item:hover {
    background-color: rgb(236, 236, 236);
    text-shadow: 0px 0px 10px rgb(69, 69, 69);
  }
</style>