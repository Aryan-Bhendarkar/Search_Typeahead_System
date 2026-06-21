# Search Typeahead System

A high-performance, real-time search autocomplete and typeahead suggestion system. Designed to provide instant search predictions as users type, it balances speed with intelligent caching and routing mechanisms under the hood.

## Screenshots

> **Note:** Drop your screenshots here.

![Search Suggestions UI](placeholder-ui.png)  
*Main search interface with real-time suggestions.*

![Debugger and Metrics](placeholder-metrics.png)  
*Live metrics dashboard and consistent hash ring visualization.*

## Key Features

* **Real-time Autocomplete:** Delivers instant, scored search suggestions with debounce handling to minimize unnecessary network requests.
* **Trending Searches:** Automatically tracks and displays the most popular queries globally.
* **Distributed Caching Strategy:** Uses a Consistent Hash Ring to intelligently route search prefixes to specific backend cache nodes, optimizing load distribution.
* **Live Analytics Dashboard:** Visualizes cache performance (hit rate, total hits/misses) and buffer accumulation in real time directly on the UI.
* **Write-Behind Caching:** Implements a buffer to batch incoming search queries before asynchronously writing them to the primary database, ensuring the system isn't bottlenecked by frequent writes.

## How It Works

The system is split into a responsive frontend and a highly optimized backend, utilizing Redis for lightning-fast data retrieval.

* **Frontend:** Built with vanilla JavaScript, HTML, and CSS. It features keyboard navigation, smooth micro-animations, and a dedicated debugger panel to visualize backend routing.
* **Consistent Hashing:** When a user types a prefix, the backend hashes the query to determine exactly which virtual cache node is responsible for serving it.
* **Data Flow:**
  1. A user types a query prefix.
  2. The request is routed to the appropriate cache node.
  3. If there is a **Cache Hit**, suggestions are returned instantly.
  4. If there is a **Cache Miss**, data is loaded from the primary store, cached on the designated node, and then returned.
  5. Successfully selected search queries are added to an in-memory buffer and flushed to the database in batches to maintain high throughput.

## UI & UX Highlights

* **Keyboard Navigation:** Full support for `Arrow Up`, `Arrow Down`, `Enter`, and `Escape` for seamless accessibility.
* **Visual Debugging:** The interface exposes backend decisions, showing exactly which node handled the request and whether it resulted in a cache hit or miss.
* **Responsive Layout:** A modern, clean design that looks great and adapts to different screen sizes.
