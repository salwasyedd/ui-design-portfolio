# Smart Closet — Project 1

By Salwa Syed

## About the Project

Smart Closet is a digital mock-up UI for a smart walk-in closet, designed and built as a UI design course project. The interface imagines a panel mounted on the outside of a closet door that helps a user decide what to wear, track their laundry, and browse their wardrobe all while not having to step inside or dig through hanger, drawers, or basekts first.

Core features:
- **Weather-based outfit suggestions** — displays the current temperature, a weather icon, and a corresponding outfit recommendation with a photo
- **Laundry status tracking** — shows clean/dirty counts per clothing category, with a low-stock alert when essentials are running out
- **Build an Outfit catalog** — a browsable, tag-filterable view of the closet's contents, similar to filtering on a shopping site

Full design process — affordances, user interviews, sketches, and
evaluation — is documented separately in
[design/design.md](design/design.md).

## Interface Walkthrough

### Weather & Outfit Suggestion
The top panel shows the current temperature, a weather icon (sun, cloud, windy-cloud, or snowflake depending on conditions), and a suggested outfit with a photo. Clicking **Simulate Weather Change** in the testing panel cycles through different conditions to preview each suggestion.

![Weather panel](docs/screenshots/weather-panel.png)

### Laundry Status
Below the weather panel, a scrollable list shows clean vs. dirty counts for each clothing category. If any category drops to 0 or 1 clean items, a red alert text appears listing what's running low.

![Laundry status](docs/screenshots/laundry-status.png)

### Build an Outfit (Catalog)
Clicking the **Build an Outfit** button opens a tag-filterable catalog of the closet's contents.

![Build an Outfit button](docs/screenshots/catalog-button.png)

Users can add filter tags (e.g. "casual," "winter") to narrow results, and remove them individually via the X on each tag chip. Each item shows a photo and when it was last worn.

![Catalog view](docs/screenshots/catalog-view.png)

### Testing Panel
For demo purposes, a Testing Panel (not part of the real device UI) lets a reviewer trigger state changes: simulate a weather change, simulate wearing an item, do laundry, or view info about the testing controls.

![Testing panel](docs/screenshots/testing-panel.png)

## Running locally
npm install
npm run dev