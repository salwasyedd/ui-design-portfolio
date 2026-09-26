<script>
  let showPlacement = false;
  let testingMode = false;
  let showInfo = false;

  function togglePlacement() {
    showPlacement = !showPlacement;
  }

  function toggleTestingMode() {
    testingMode = !testingMode;
  }

  function toggleInfo() {
    showInfo = !showInfo;
  }

  function getGreeting() {
    const hour = new Date().getHours();
    if (hour < 12) return "Good morning";
    if (hour < 18) return "Good afternoon";
    return "Good evening";
  }

  const suggestions = [
    { temp: 45, text: "It's chilly: wear the gray hoodie.", outfit: "Gray hoodie + jeans" },
    { temp: 62, text: "Mild out: a light jacket works.", outfit: "Light jacket + tee" },
    { temp: 78, text: "Warm today: go with a t-shirt.", outfit: "White t-shirt + shorts" },
    { temp: 33, text: "Cold! Grab the winter coat.", outfit: "Winter coat + scarf" }
  ];

  let currentSuggestion = suggestions[0];

  function getNewSuggestion() {
    const random = suggestions[Math.floor(Math.random() * suggestions.length)];
    currentSuggestion = random;
  }


  let laundry = [
    { category: "Socks", clean: 3, dirty: 2 },
    { category: "Shirts", clean: 6, dirty: 1 },
    { category: "Sweatpants", clean: 1, dirty: 3 },
    { category: "Jeans", clean: 2, dirty: 1 },
    { category: "Underwear", clean: 4, dirty: 0 },
    { category: "Jackets", clean: 2, dirty: 0 }
  ];

  const LOW_STOCK_THRESHOLD = 1;

  $: lowStockItems = laundry.filter(item => item.clean <= LOW_STOCK_THRESHOLD);

  function doLaundry() {
    laundry = laundry.map(item => ({
      category: item.category,
      clean: item.clean + item.dirty,
      dirty: 0
    }));
  }

  function simulateWear() {
    const wearable = laundry.filter(item => item.clean > 0);
    if (wearable.length === 0) return;
    const pick = wearable[Math.floor(Math.random() * wearable.length)];
    laundry = laundry.map(item =>
      item.category === pick.category
        ? { ...item, clean: item.clean - 1, dirty: item.dirty + 1 }
        : item
    );
  }
</script>

<main>
  <div class="page">

    <header>
      <div class="title-block">
        <h1>Smart Closet</h1>
        <p class="byline">Salwa Syed</p>
      </div>
      <div class="header-links">
        <button class="link-btn" on:click={togglePlacement}>Where does this go?</button>
        <a href="https://github.com/salwasyedd/ui-design-portfolio/blob/main/project1-smart-closet/design/design.md" target="_blank" class="writeup-link">
          Project Write-Up
        </a>
      </div>
    </header>

    {#if showPlacement}
      <div class="placement-block">
        <img src="/src/lib/hybrid-sketch.jpg" alt="Hybrid sketch showing the smart closet UI overlaid on the physical closet door" class="placement-img">
        <p class="placement-caption">This panel is mounted on the outside of the closet door.</p>
      </div>
    {/if}

    <p class="greeting">{getGreeting()}</p>

    <!-- device ui region -->
    <section class="device-ui weather-panel">
      <div class="weather-row">
        <div class="weather-info">
          <div class="temp-row">
            <span class="temp">{currentSuggestion.temp}&deg;</span>
            <span class="weather-icon"></span>
          </div>
          <p class="suggestion-text">{currentSuggestion.text}</p>
        </div>

        <div class="outfit-box">
          <p class="outfit-label">Suggested Outfit</p>
          <p class="outfit-name">{currentSuggestion.outfit}</p>
        </div>
      </div>
    </section>

      <section class="device-ui laundry-panel">
        <div class="laundry-section">
          <div class="laundry-header">
            <p class="section-label">Laundry Status</p>
            <span class="status-dot" class:low={lowStockItems.length > 0}></span>
          </div>

          <div class="laundry-list">
          {#each laundry as item}
            <div class="laundry-row">
              <span class="laundry-category">{item.category}</span>
              <span class="laundry-counts">{item.clean} clean, {item.dirty} dirty</span>
            </div>
          {/each}
        </div>

        {#if lowStockItems.length > 0}
          <p class="laundry-alert">
            Low on: {lowStockItems.map(i => i.category).join(", ")}
          </p>
        {/if}
      </div>

      <!-- level 2+ controls will be added here -->
    </section>

    <div class="testing-toggle-row">
      <button class="link-btn" on:click={toggleTestingMode}>
        {testingMode ? "Hide Testing Mode" : "Testing Mode"}
      </button>
    </div>

    {#if testingMode}
      <aside class="testing-ui">
        <p class="region-label">Testing Panel</p>

        <div class="testing-controls">
          <button class="btn-secondary" on:click={toggleInfo}>Info</button>
          <button class="btn-primary" on:click={getNewSuggestion}>Simulate Weather Change</button>
          <button class="btn-primary" on:click={simulateWear}>Simulate Wearing an Item</button>
          <button class="btn-primary" on:click={doLaundry}>Do Laundry</button>
        </div>

        {#if showInfo}
          <p class="info-text">
            This panel simulates using the smart closet. Trigger changes
            here and watch the Device UI above respond.
          </p>
        {/if}

        <!-- test buttons for level 1+ will be added here -->
      </aside>
    {/if}

  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    background-color: #EDE7DC;
  }

  main {
    font-family: 'Inter', sans-serif;
    padding: 48px 24px;
    display: flex;
    justify-content: center;
  }

  .page {
    width: 100%;
    max-width: 640px;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    border-bottom: 1px solid #D8CFBE;
    padding-bottom: 20px;
    margin-bottom: 32px;
  }

  h1 {
    font-family: 'Fraunces', serif;
    font-size: 34px;
    font-weight: 600;
    color: #3A322C;
    margin: 0;
  }

  .byline {
    font-size: 14px;
    color: #8A8072;
    margin: 4px 0 0 0;
  }

  .header-links {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 6px;
  }

  .writeup-link {
    font-size: 13px;
    color: #6B7059;
    text-decoration: none;
    border-bottom: 1px solid #6B7059;
  }

  .link-btn {
    background: none;
    border: none;
    font-family: 'Inter', sans-serif;
    font-size: 13px;
    color: #8A8072;
    text-decoration: underline;
    cursor: pointer;
    padding: 0;
  }

  .placement-block {
    background-color: #FBF9F5;
    border: 1px solid #D8CFBE;
    border-radius: 12px;
    padding: 16px;
    margin-bottom: 24px;
    display: flex;
    align-items: center;
    gap: 14px;
  }

  .placement-img {
    max-width: 140px;
    border-radius: 6px;
  }

  .placement-caption {
    font-size: 13px;
    color: #5C5449;
    margin: 0;
  }

  .greeting {
    font-family: 'Fraunces', serif;
    font-size: 22px;
    color: #3A322C;
    margin: 0 0 16px 0;
  }

  .device-ui {
    background-color: #FBF9F5;
    border: 1px solid #D8CFBE;
    border-radius: 16px;
    padding: 32px;
  }

  .weather-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
}

  .weather-info {
    flex: 1;
  }

  .temp-row {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .temp {
    font-family: 'Fraunces', serif;
    font-size: 48px;
    font-weight: 500;
    color: #3A322C;
  }

  .weather-icon {
    width: 22px;
    height: 22px;
    border: 2px solid #A9967C;
    border-radius: 50%;
  }

  .suggestion-text {
    font-size: 15px;
    color: #5C5449;
    margin-top: 8px;
  }

  .outfit-box {
    background-color: #EDE7DC;
    border: 1px solid #D8CFBE;
    border-radius: 12px;
    padding: 16px;
    min-width: 150px;
    text-align: center;
  }

  .outfit-label {
    font-size: 11px;
    letter-spacing: 0.04em;
    color: #8A8072;
    margin: 0 0 8px 0;
  }

  .outfit-name {
    font-size: 14px;
    color: #3A322C;
    font-weight: 500;
    margin: 0;
  }

  .testing-toggle-row {
    text-align: center;
    margin-top: 20px;
  }

  .testing-ui {
    background-color: #E3DED2;
    border: 1px solid #CFC6B3;
    border-radius: 16px;
    padding: 24px;
    margin-top: 16px;
  }

  .region-label {
    font-size: 12px;
    letter-spacing: 0.04em;
    color: #8A8072;
    margin: 0 0 16px 0;
  }

  .testing-controls {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  button {
    font-family: 'Inter', sans-serif;
    font-size: 14px;
    padding: 10px 14px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
  }

  .btn-primary {
    background-color: #6B7059;
    color: #FBF9F5;
  }

  .btn-secondary {
    background-color: transparent;
    border: 1px solid #8A8072;
    color: #5C5449;
  }

  .info-text {
    font-size: 13px;
    color: #5C5449;
    margin-top: 14px;
    line-height: 1.5;
  }

  .laundry-section {
  margin-top: 28px;
  padding-top: 24px;
  border-top: 1px solid #D8CFBE;
}

.laundry-header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 12px;
}

.section-label {
  font-size: 11px;
  letter-spacing: 0.04em;
  color: #8A8072;
  margin: 0;
}

.status-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: #6B7059;
}

.status-dot.low {
  background-color: #B25D45;
}

.laundry-list {
  max-height: 130px;
  overflow-y: auto;
  padding-right: 8px;
}

.laundry-row {
  display: flex;
  justify-content: space-between;
  font-size: 14px;
  color: #3A322C;
  padding: 6px 0;
  border-bottom: 1px solid #EDE7DC;
}

.laundry-counts {
  color: #5C5449;
}

.laundry-alert {
  font-size: 13px;
  color: #B25D45;
  margin-top: 10px;
}
.weather-panel {
  margin-bottom: 20px;
}

.laundry-section {
  margin-top: 0;
  padding-top: 0;
  border-top: none;
}
</style>