<script>
  let showInfo = false;

  function toggleInfo() {
    showInfo = !showInfo;
  }
</script>

<main>
  <header>
    <h1>Smart Closet</h1>
    <p>by Salwa Syed</p>
    <img src="/src/lib/closet-placement.jpeg" alt="Diagram showing UI panel placement on the outside of the closet door" style="max-width: 200px; display: block; margin-bottom: 10px;">
    <p><a href="https://github.com/salwasyedd/ui-design-portfolio/blob/main/project1-smart-closet/design/design.md" target="_blank">Project Write-Up</a></p>
  </header>

  <div class="layout">

    <!-- device ui region -->
    <section class="device-ui">
      <h2>Device UI (Closet Interface)</h2>
      <p><em>This is where the closet's own controls and display will go.</em></p>
      <!-- level 1+ controls will be added here -->
    </section>

    <!-- testing/info region -->
    <section class="testing-ui">
      <h2>Testing Panel</h2>

      <button on:click={toggleInfo}>Info</button>
      {#if showInfo}
        <p>
          This panel lets you simulate using the smart closet.
          Use the buttons here to trigger changes (like turning
          on the light or opening the closet door) and watch the
          Device UI on the left respond.
        </p>
      {/if}

      <!-- test buttons for level 1+ will be added here -->
    </section>

  </div>
</main>

<style>
  main {
    font-family: sans-serif;
    padding: 20px;
  }
  .layout {
    display: flex;
    gap: 20px;
    margin-top: 20px;
  }
  .device-ui, .testing-ui {
    border: 2px solid #444;
    border-radius: 10px;
    padding: 15px;
    flex: 1;
    min-height: 300px;
  }
  .device-ui {
    background-color: #f4f4f4;
  }
  .testing-ui {
    background-color: #eef6ff;
  }
</style>