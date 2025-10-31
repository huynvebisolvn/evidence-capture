# Evidence

Evidence capture

## Live Deployment

- **GitHub Pages**: https://huynvebisolvn.github.io/evidence-capture/
- **Render (Dev)**: https://evcapture.onrender.com/

## Project Setup

```sh
yarn install
```

### Compile and Hot-Reload for Development

```sh
yarn dev
```

### Type-Check, Compile and Minify for Production

```sh
yarn build
```

## Deployment

The application is automatically deployed to GitHub Pages when changes are pushed to the main branch. The deployment workflow:

1. Installs dependencies using Yarn
2. Builds the production bundle
3. Deploys to GitHub Pages

To enable GitHub Pages deployment:
1. Go to repository Settings → Pages
2. Under "Build and deployment", select "GitHub Actions" as the source
3. Push to the main branch or manually trigger the workflow
