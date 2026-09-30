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
    {
      temp: 45,
      text: "It's chilly: wear the gray hoodie.",
      outfit: "Gray hoodie + jeans",
      img: "/catalog/gray-hoodie.jpg",
      condition: "breezy-cloudy",
    },
    {
      temp: 62,
      text: "Mild out: a light sweater works.",
      outfit: "Green sweater + jeans",
      img: "/catalog/green-sweater.jpg",
      condition: "cloudy",
    },
    {
      temp: 78,
      text: "Warm today: go with a t-shirt.",
      outfit: "White t-shirt + shorts",
      img: "/catalog/white-tshirt.jpg",
      condition: "sunny",
    },
    {
      temp: 33,
      text: "Cold! Grab the winter coat.",
      outfit: "Winter coat + scarf",
      img: "/catalog/winter-coat.jpg",
      condition: "snow",
    },
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
    { category: "Jackets", clean: 2, dirty: 0 },
  ];

  const LOW_STOCK_THRESHOLD = 1;

  $: lowStockItems = laundry.filter(
    (item) => item.clean <= LOW_STOCK_THRESHOLD,
  );

  function doLaundry() {
    laundry = laundry.map((item) => ({
      category: item.category,
      clean: item.clean + item.dirty,
      dirty: 0,
    }));
  }

  function simulateWear() {
    const wearable = laundry.filter((item) => item.clean > 0);
    if (wearable.length === 0) return;
    const pick = wearable[Math.floor(Math.random() * wearable.length)];
    laundry = laundry.map((item) =>
      item.category === pick.category
        ? { ...item, clean: item.clean - 1, dirty: item.dirty + 1 }
        : item,
    );
  }

  const catalogItems = [
    {
      name: "Gray Hoodie",
      tags: ["casual", "winter"],
      lastWorn: "2 days ago",
      img: "/catalog/gray-hoodie.jpg",
    },
    {
      name: "White T-Shirt",
      tags: ["casual", "summer"],
      lastWorn: "1 day ago",
      img: "/catalog/white-tshirt.jpg",
    },
    {
      name: "Work Blazer",
      tags: ["work", "formal"],
      lastWorn: "1 week ago",
      img: "/catalog/work-blazer.jpg",
    },
    {
      name: "Blue Jeans",
      tags: ["casual"],
      lastWorn: "3 days ago",
      img: "/catalog/blue-jeans.jpg",
    },
    {
      name: "Winter Coat",
      tags: ["winter", "formal"],
      lastWorn: "1 month ago",
      img: "/catalog/winter-coat.jpg",
    },
    {
      name: "Green Sweater",
      tags: ["green", "winter"],
      lastWorn: "5 days ago",
      img: "/catalog/green-sweater.jpg",
    },
    {
      name: "Black Dress Pants",
      tags: ["work", "formal"],
      lastWorn: "4 days ago",
      img: "/catalog/black-dress-pants.jpg",
    },
    {
      name: "Sneakers",
      tags: ["casual", "summer"],
      lastWorn: "today",
      img: "/catalog/sneakers.jpg",
    },
  ];

  let activeTags = [];
  let showCatalog = false;

  function toggleCatalog() {
    showCatalog = !showCatalog;
  }

  function addTag(tag) {
    if (!activeTags.includes(tag)) {
      activeTags = [...activeTags, tag];
    }
  }

  function removeTag(tag) {
    activeTags = activeTags.filter((t) => t !== tag);
  }

  $: filteredItems =
    activeTags.length === 0
      ? catalogItems
      : catalogItems.filter((item) =>
          activeTags.every((tag) => item.tags.includes(tag)),
        );

  $: allTags = [...new Set(catalogItems.flatMap((item) => item.tags))];
</script>

<main>
  <div class="page">
    <header>
      <div class="title-block">
        <h1>Smart Closet</h1>
        <p class="byline">Salwa Syed</p>
      </div>
      <div class="header-links">
        <button class="link-btn" on:click={togglePlacement}
          >Where does this go?</button
        >
        <a
          href="https://github.com/salwasyedd/ui-design-portfolio/blob/main/project1-smart-closet/design/design.md"
          target="_blank"
          class="writeup-link"
        >
          Project Write-Up
        </a>
      </div>
    </header>

    {#if showPlacement}
      <div class="placement-block">
        <img
          src="/hybrid-sketch.jpg"
          alt="Hybrid sketch showing the smart closet UI overlaid on the physical closet door"
          class="placement-img"
        />
        <p class="placement-caption">
          This panel is mounted on the outside of the closet door.
        </p>
      </div>
    {/if}

    <p class="greeting">{getGreeting()}</p>

    <section class="device-ui weather-panel">
      <div class="weather-row">
        <div class="weather-info">
          <div class="temp-row">
            <span class="temp">{currentSuggestion.temp}&deg;</span>
            <span class="weather-icon">
              {#if currentSuggestion.condition === "sunny"}
                <svg
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  ><circle cx="12" cy="12" r="5" /><line
                    x1="12"
                    y1="1"
                    x2="12"
                    y2="3"
                  /><line x1="12" y1="21" x2="12" y2="23" /><line
                    x1="4.22"
                    y1="4.22"
                    x2="5.64"
                    y2="5.64"
                  /><line x1="18.36" y1="18.36" x2="19.78" y2="19.78" /><line
                    x1="1"
                    y1="12"
                    x2="3"
                    y2="12"
                  /><line x1="21" y1="12" x2="23" y2="12" /><line
                    x1="4.22"
                    y1="19.78"
                    x2="5.64"
                    y2="18.36"
                  /><line x1="18.36" y1="5.64" x2="19.78" y2="4.22" /></svg
                >
              {:else if currentSuggestion.condition === "cloudy"}
                <svg
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  ><path
                    d="M17.5 19H9a5 5 0 1 1 1-9.9A6 6 0 0 1 21 12a4 4 0 0 1-3.5 7z"
                  /></svg
                >
              {:else if currentSuggestion.condition === "breezy-cloudy"}
                <svg
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  ><path
                    d="M14.5 16H6a4 4 0 1 1 .8-7.9A5 5 0 0 1 17 10a3.5 3.5 0 0 1-2.5 6z"
                  /><line x1="3" y1="19" x2="11" y2="19" /><line
                    x1="3"
                    y1="21.5"
                    x2="9"
                    y2="21.5"
                  /></svg
                >
              {:else if currentSuggestion.condition === "snow"}
                <svg
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="1.4"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <g>
                    <line x1="12" y1="12" x2="12" y2="3" />
                    <line x1="12" y1="8" x2="10.3" y2="6.2" />
                    <line x1="12" y1="8" x2="13.7" y2="6.2" />
                    <line x1="12" y1="5.3" x2="11" y2="4.2" />
                    <line x1="12" y1="5.3" x2="13" y2="4.2" />
                  </g>
                  <g transform="rotate(60 12 12)">
                    <line x1="12" y1="12" x2="12" y2="3" />
                    <line x1="12" y1="8" x2="10.3" y2="6.2" />
                    <line x1="12" y1="8" x2="13.7" y2="6.2" />
                    <line x1="12" y1="5.3" x2="11" y2="4.2" />
                    <line x1="12" y1="5.3" x2="13" y2="4.2" />
                  </g>
                  <g transform="rotate(120 12 12)">
                    <line x1="12" y1="12" x2="12" y2="3" />
                    <line x1="12" y1="8" x2="10.3" y2="6.2" />
                    <line x1="12" y1="8" x2="13.7" y2="6.2" />
                    <line x1="12" y1="5.3" x2="11" y2="4.2" />
                    <line x1="12" y1="5.3" x2="13" y2="4.2" />
                  </g>
                  <g transform="rotate(180 12 12)">
                    <line x1="12" y1="12" x2="12" y2="3" />
                    <line x1="12" y1="8" x2="10.3" y2="6.2" />
                    <line x1="12" y1="8" x2="13.7" y2="6.2" />
                    <line x1="12" y1="5.3" x2="11" y2="4.2" />
                    <line x1="12" y1="5.3" x2="13" y2="4.2" />
                  </g>
                  <g transform="rotate(240 12 12)">
                    <line x1="12" y1="12" x2="12" y2="3" />
                    <line x1="12" y1="8" x2="10.3" y2="6.2" />
                    <line x1="12" y1="8" x2="13.7" y2="6.2" />
                    <line x1="12" y1="5.3" x2="11" y2="4.2" />
                    <line x1="12" y1="5.3" x2="13" y2="4.2" />
                  </g>
                  <g transform="rotate(300 12 12)">
                    <line x1="12" y1="12" x2="12" y2="3" />
                    <line x1="12" y1="8" x2="10.3" y2="6.2" />
                    <line x1="12" y1="8" x2="13.7" y2="6.2" />
                    <line x1="12" y1="5.3" x2="11" y2="4.2" />
                    <line x1="12" y1="5.3" x2="13" y2="4.2" />
                  </g>
                </svg>
              {/if}
            </span>
          </div>
          <p class="suggestion-text">{currentSuggestion.text}</p>
        </div>

        <div class="outfit-box">
          <img
            src={currentSuggestion.img}
            alt={currentSuggestion.outfit}
            class="outfit-photo"
          />
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
              <span class="laundry-counts"
                >{item.clean} clean, {item.dirty} dirty</span
              >
            </div>
          {/each}
        </div>

        {#if lowStockItems.length > 0}
          <p class="laundry-alert">
            Low on: {lowStockItems.map((i) => i.category).join(", ")}
          </p>
        {/if}
      </div>

    </section>

    <div class="outfit-btn-row">
      <button class="btn-outfit" on:click={toggleCatalog}>
        {showCatalog ? "Close Catalog" : "Build an Outfit"}
      </button>
    </div>

    {#if showCatalog}
      <section class="device-ui catalog-panel">
        <p class="section-label">Your Closet</p>

        <div class="active-tags">
          {#each activeTags as tag}
            <span class="tag-chip active">
              {tag}
              <button class="tag-remove" on:click={() => removeTag(tag)}
                >&times;</button
              >
            </span>
          {/each}
        </div>

        <div class="tag-options">
          {#each allTags as tag}
            {#if !activeTags.includes(tag)}
              <button class="tag-chip" on:click={() => addTag(tag)}
                >{tag}</button
              >
            {/if}
          {/each}
        </div>

        <div class="catalog-grid">
          {#each filteredItems as item}
            <div class="catalog-item">
              <img src={item.img} alt={item.name} class="item-photo" />
              <p class="item-name">{item.name}</p>
              <p class="item-last-worn">Last worn: {item.lastWorn}</p>
            </div>
          {/each}
        </div>

        {#if filteredItems.length === 0}
          <p class="no-results">No items match these tags.</p>
        {/if}
      </section>
    {/if}

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
          <button class="btn-primary" on:click={getNewSuggestion}
            >Simulate Weather Change</button
          >
          <button class="btn-primary" on:click={simulateWear}
            >Simulate Wearing an Item</button
          >
          <button class="btn-primary" on:click={doLaundry}>Do Laundry</button>
        </div>

        {#if showInfo}
          <p class="info-text">
            This panel simulates using the smart closet. Trigger changes here
            and watch the Device UI above respond.
          </p>
        {/if}

      </aside>
    {/if}
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    background-color: #ede7dc;
  }

  main {
    font-family: "Inter", sans-serif;
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
    border-bottom: 1px solid #d8cfbe;
    padding-bottom: 12px;
    margin-bottom: 20px;
  }

  h1 {
    font-family: "Fraunces", serif;
    font-size: 34px;
    font-weight: 600;
    color: #3a322c;
    margin: 0;
  }

  .byline {
    font-size: 14px;
    color: #8a8072;
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
    color: #6b7059;
    text-decoration: none;
    border-bottom: 1px solid #6b7059;
  }

  .link-btn {
    background: none;
    border: none;
    font-family: "Inter", sans-serif;
    font-size: 13px;
    color: #8a8072;
    text-decoration: underline;
    cursor: pointer;
    padding: 0;
  }

  .placement-block {
    background-color: #fbf9f5;
    border: 1px solid #d8cfbe;
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
    color: #5c5449;
    margin: 0;
  }

  .greeting {
    font-family: "Fraunces", serif;
    font-size: 22px;
    color: #3a322c;
    margin: 0 0 10px 0;
  }

  .device-ui {
    background-color: #fbf9f5;
    border: 1px solid #d8cfbe;
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
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .temp-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
  }

  .temp {
    font-family: "Fraunces", serif;
    font-size: 48px;
    font-weight: 500;
    color: #3a322c;
  }

  .weather-icon {
    width: 34px;
    height: 34px;
    color: #a9967c;
    display: inline-flex;
  }

  .weather-icon svg {
    width: 100%;
    height: 100%;
  }

  .suggestion-text {
    font-size: 19px;
    color: #5c5449;
    margin-top: 16px;
  }

  .outfit-box {
    background-color: #ede7dc;
    border: 1px solid #d8cfbe;
    border-radius: 12px;
    padding: 16px;
    min-width: 150px;
    text-align: center;
  }

  .outfit-photo {
    width: 100%;
    max-width: 90px;
    height: 70px;
    object-fit: cover;
    border: 1px solid #d8cfbe;
    border-radius: 8px;
    margin: 0 auto 10px auto;
    display: block;
  }

  .outfit-label {
    font-size: 11px;
    letter-spacing: 0.04em;
    color: #8a8072;
    margin: 0 0 8px 0;
  }

  .outfit-name {
    font-size: 14px;
    color: #3a322c;
    font-weight: 500;
    margin: 0;
  }

  .testing-toggle-row {
    text-align: center;
    margin-top: 20px;
  }

  .outfit-btn-row {
    text-align: center;
    margin-top: 20px;
  }

  .btn-outfit {
    width: 100%;
    max-width: 320px;
    background-color: #6b7059;
    color: #fbf9f5;
    font-family: "Inter", sans-serif;
    font-size: 15px;
    font-weight: 500;
    padding: 14px 20px;
    border-radius: 14px;
    border: none;
    cursor: pointer;
  }

  .testing-ui {
    background-color: #e3ded2;
    border: 1px solid #cfc6b3;
    border-radius: 16px;
    padding: 24px;
    margin-top: 16px;
  }

  .region-label {
    font-size: 12px;
    letter-spacing: 0.04em;
    color: #8a8072;
    margin: 0 0 16px 0;
  }

  .testing-controls {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  button {
    font-family: "Inter", sans-serif;
    font-size: 14px;
    padding: 10px 14px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
  }

  .btn-primary {
    background-color: #6b7059;
    color: #fbf9f5;
  }

  .btn-secondary {
    background-color: transparent;
    border: 1px solid #8a8072;
    color: #5c5449;
  }

  .info-text {
    font-size: 13px;
    color: #5c5449;
    margin-top: 14px;
    line-height: 1.5;
  }

  .laundry-section {
    margin-top: 28px;
    padding-top: 24px;
    border-top: 1px solid #d8cfbe;
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
    color: #8a8072;
    margin: 0;
  }

  .status-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: #6b7059;
  }

  .status-dot.low {
    background-color: #b25d45;
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
    color: #3a322c;
    padding: 6px 0;
    border-bottom: 1px solid #ede7dc;
  }

  .laundry-counts {
    color: #5c5449;
  }

  .laundry-alert {
    font-size: 13px;
    color: #b25d45;
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

  .catalog-panel {
    margin-top: 20px;
  }

  .active-tags,
  .tag-options {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 12px;
  }

  .tag-chip {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background-color: #ede7dc;
    border: 1px solid #d8cfbe;
    border-radius: 20px;
    padding: 6px 12px;
    font-size: 13px;
    color: #5c5449;
    cursor: pointer;
  }

  .tag-chip.active {
    background-color: #6b7059;
    color: #fbf9f5;
    border-color: #6b7059;
  }

  .tag-remove {
    background: none;
    border: none;
    color: inherit;
    font-size: 14px;
    cursor: pointer;
    padding: 0;
  }

  .catalog-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 14px;
    margin-top: 16px;
  }

  .catalog-item {
    text-align: center;
  }

  .item-photo {
    width: 100%;
    height: 90px;
    object-fit: cover;
    border: 1px solid #d8cfbe;
    border-radius: 8px;
    margin-bottom: 6px;
    display: block;
  }

  .item-name {
    font-size: 13px;
    color: #3a322c;
    margin: 0;
  }

  .item-last-worn {
    font-size: 11px;
    color: #8a8072;
    margin: 2px 0 0 0;
  }

  .no-results {
    font-size: 13px;
    color: #8a8072;
    margin-top: 12px;
  }
</style>
