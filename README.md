# CoinDash — Live Crypto Tracker

CoinDash is a polished single-page cryptocurrency dashboard built for a college club recruitment project. It provides a focused way to explore market data, view trending assets, and curate a personal watchlist using live data from the public CoinGecko API.

The interface uses a dark terminal-inspired visual system with neon lime and lilac accents, responsive layouts, animated transitions, hover depth, and lightweight SVG sparklines.

## Features

- Animated three-second splash screen built with `useEffect` and `setTimeout`.
- Market Overview panel with market statistics, asset cards, market-cap table, and search filtering.
- Trending panel sorted by 24-hour percentage change.
- Watchlist panel with add/remove star interactions and ticker copying.
- Live cryptocurrency data from CoinGecko's public `/coins/markets` endpoint.
- Loading, API error, retry, fallback-data, and no-search-results states.
- Responsive sidebar navigation with a mobile drawer layout.
- Hover-lift effects, responsive cards, SVG sparklines, and reduced-motion support.
- No backend, database, authentication, API key, React Router, or Next.js dependency is required.

## Technology

| Area | Technology |
| --- | --- |
| Frontend | React 19 with TypeScript-compatible JSX |
| Build tool | Vite |
| Styling | Tailwind CSS 4 with custom CSS design tokens |
| Icons | Lucide React |
| Market data | CoinGecko public API |
| Navigation | React state-based tabs using `useState` |
| Data loading | Browser `fetch` with `useEffect` |
| Deployment | Netlify or any static hosting provider |

## Requirements

Install the following before running the project locally:

- Node.js 18 or newer.
- npm 9 or newer.
- An internet connection for live CoinGecko data.

## Local setup

Clone the repository and open the project directory:

```bash
git clone <your-github-repository-url>
cd coindash-live-crypto-tracker
```

Install dependencies with the legacy peer-dependency option. The project includes a Vite plugin whose peer dependency declaration targets older Vite versions, so this option avoids an npm dependency-resolution failure:

```bash
npm install --legacy-peer-deps
```

Create a `.env` file in the project root. The root is the same directory as `package.json`:

```env
VITE_COINGECKO_API_URL=https://api.coingecko.com/api/v3
```

Start the development server:

```bash
npm run dev
```

Open the local URL printed by Vite. It is usually:

```text
http://localhost:5173
```

The environment variable is optional because the application includes the same CoinGecko URL as a fallback. It is still recommended for local configuration and deployment consistency.

## Available commands

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start the Vite development server. |
| `npm run build` | Create the production build. |
| `npm run preview` | Preview the production build locally. |
| `npm run check` | Run the TypeScript compiler without emitting files. |
| `npm run format` | Format project files with Prettier. |
| `npx vitest run client/src/coingecko-env.test.ts` | Verify the configured CoinGecko endpoint. |

To stop the development server, press `Ctrl + C` in the terminal.

## Production build

Run the following commands:

```bash
npm run build
npm run preview
```

The Vite frontend is generated in:

```text
dist/public
```

The project also generates a small server bundle in `dist`, but CoinDash is designed as a client-only frontend for static hosting.

## Deploying to Netlify

This repository includes a `netlify.toml` file and a `client/public/_redirects` file for Netlify deployment.

When configuring a Netlify site, use these values:

| Netlify setting | Value |
| --- | --- |
| Base directory | Leave empty |
| Build command | `npm run build` |
| Publish directory | `dist/public` |
|

Add this environment variable in Netlify under **Site configuration → Environment variables**:

```text
VITE_COINGECKO_API_URL=https://api.coingecko.com/api/v3
```

The repository already sets the npm install flag in `netlify.toml`:

```toml
[build.environment]
  NPM_FLAGS = "--legacy-peer-deps"
```

If you deploy manually instead of connecting a Git repository, run `npm run build` and upload the `dist/public` folder. Do not upload only the `dist` folder or the `client` source folder.

## Project structure

```text
coindash-live-crypto-tracker/
├── client/
│   ├── public/
│   │   └── _redirects
│   ├── src/
│   │   ├── App.tsx
│   │   ├── coingecko-env.test.ts
│   │   ├── index.css
│   │   └── main.tsx
│   └── index.html
├── netlify.toml
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

## API and fallback behavior

CoinDash requests market data from the CoinGecko public API. No CoinGecko API key is required for the current implementation.

If the API request fails or is rate-limited, the application displays a friendly error state and keeps a small fallback dataset available so the dashboard remains explorable. The fallback values are demonstration data and should not be used for financial decisions.

## Troubleshooting

### npm shows `ERESOLVE unable to resolve dependency tree`

Run:

```bash
npm install --legacy-peer-deps
```

The same option is already configured for Netlify through `netlify.toml`.

### Netlify shows a 404

Confirm the following settings:

```text
Base directory:      empty
Build command:       npm run build
Publish directory:   dist/public
```

Also confirm that `netlify.toml` and `client/public/_redirects` are committed and pushed to the connected repository.

### Live prices are not loading

Confirm that the device has internet access, the CoinGecko API is reachable, and the environment variable is spelled exactly as follows:

```text
VITE_COINGECKO_API_URL
```

Restart the development server after changing `.env` because Vite reads environment variables when it starts.

### Port 5173 is already in use

Vite may automatically choose another available port. Always open the exact URL printed in the terminal.

## Limitations

CoinDash is an educational frontend project. It does not execute trades, manage wallets, store user accounts, or provide financial advice. Watchlist data is held in React state and is reset when the page is reloaded.

## License

This project is available for educational and portfolio use. Add a repository-specific license before distributing it as an open-source project.

## References

[1]: https://www.coingecko.com/en/api "CoinGecko API documentation"
[2]: https://vite.dev/guide/ "Vite documentation"
[3]: https://react.dev/reference/react "React API reference"
[4]: https://docs.netlify.com/configure-builds/file-based-configuration/ "Netlify file-based configuration documentation"
