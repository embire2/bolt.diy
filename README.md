# bolt.gives

An open-source AI coding agent that lets you interact with a remote tmux session and freely edit code in any git repository. Built with React, Vite, Cloudflare Pages, and Electron.

## Features

- **AI-Powered Development**: Chat with AI to create, edit, and run code
- **Real-time Collaboration**: Multiple users can work on the same project
- **Session Management**: Save, resume, and share your coding sessions
- **Cloud & Local Models**: Support for multiple AI providers including local models
- **Deployment Ready**: Deploy to Vercel, Netlify, and other platforms
- **Cross-Platform**: Runs in the browser or as a desktop app (Electron)

## v1.0.0 Release Notes

### Major Features

- **Real-time collaboration via Yjs (y-websocket)** with persisted docs and health endpoint
- **Plan/Act agent workflow** with checkpointed execution and revert support
- **Multi-provider model support** (cloud + local) with in-app model orchestrator
- **Session save/resume/share** (optional Supabase-backed storage)
- **Deployment wizard** + provider integrations (GitHub/GitLab + Vercel/Netlify)
- **Cloudflare Pages-compatible** production builds (wrangler.toml, functions/[[path]].ts)
- **Cloudflare build OOM mitigation**: NODE_OPTIONS=--max-old-space-size=6142 (or `pnpm run build:highmem`)

### New in This Version

- Complete rebranding to "bolt.gives" with backward compatibility
- Enhanced cloud deployment support
- Improved performance optimizations
- Expanded AI provider integrations
- Better documentation and setup guides

## Deploying to Cloudflare Pages

bolt.gives is designed to run on Cloudflare Pages. Follow these steps to deploy:

### Prerequisites

- A Cloudflare account
- Wrangler CLI installed (`npm install -g wrangler`)
- Your AI provider API keys ready

### Environment Variables

Set the following environment variables in your Cloudflare Pages project:

```bash
# AI Provider API Keys
ANTHROPIC_API_KEY=your_key_here
OPENAI_API_KEY=your_key_here
GOOGLE_GENERATIVE_AI_API_KEY=your_key_here
# ... add other providers you want to use

# Optional Integrations
VITE_GITHUB_ACCESS_TOKEN=your_github_token
VITE_GITLAB_ACCESS_TOKEN=your_gitlab_token
VITE_VERCEL_ACCESS_TOKEN=your_vercel_token
VITE_NETLIFY_ACCESS_TOKEN=your_netlify_token
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_key
```

### Build Command

For most deployments, use:
```bash
pnpm run build
```

### High Memory Build (Recommended)

If you encounter build OOM (Out of Memory) errors, use the high-memory build:
```bash
pnpm run build:highmem
```

Or set the build command with increased Node heap size:
```bash
NODE_OPTIONS=--max-old-space-size=6142 pnpm run build
```

### Build Output Directory

Set the build output directory to: `build/client`

### Functions Directory

Set the functions directory to: `functions`

### Node.js Version

Set the Node.js version to: `18.18` or higher

### Deployment Steps

1. Push your code to a Git repository (GitHub, GitLab, etc.)

2. In Cloudflare Pages:
   - Connect your repository
   - Set build settings:
     - Build command: `pnpm run build` or `pnpm run build:highmem`
     - Build output directory: `build/client`
     - Functions directory: `functions`
     - Node.js version: `18.18` or higher

3. Add environment variables in the Cloudflare Pages dashboard

4. Deploy!

### Troubleshooting

- **OOM Errors**: Use `pnpm run build:highmem` or set `NODE_OPTIONS=--max-old-space-size=6142`
- **Build Failures**: Check that Node.js version is 18.18 or higher
- **Function Errors**: Verify the functions directory is set to `functions`

### Local Development with Cloudflare

Test your Cloudflare Pages deployment locally:

```bash
pnpm run build
pnpm run start
```

This will use Wrangler to serve your build locally with the same environment as Cloudflare Pages.

## Getting Started

### Prerequisites

- Node.js 18.18 or higher
- pnpm (recommended) or npm

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/stackblitz-labs/bolt.gives.git
   cd bolt.gives
   ```

2. Install dependencies:
   ```bash
   pnpm install
   ```

3. Copy the environment variables:
   ```bash
   cp .env.example .env.local
   ```

4. Edit `.env.local` and add your API keys

5. Start the development server:
   ```bash
   pnpm run dev
   ```

6. Open your browser to `http://localhost:5173`

### Available Scripts

- `pnpm run dev` - Start development server
- `pnpm run build` - Build for production
- `pnpm run build:highmem` - Build for production with increased memory
- `pnpm run start` - Start production server locally
- `pnpm run lint` - Run ESLint
- `pnpm run typecheck` - Run TypeScript type checking
- `pnpm test` - Run tests
- `pnpm run electron:dev` - Start Electron development app

## Architecture

- **Frontend**: React 18 + Remix v2
- **Styling**: UnoCSS with Tailwind compatibility
- **Editor**: CodeMirror 6
- **Terminal**: xterm.js
- **AI**: Vercel AI SDK with multiple provider support
- **Deployment**: Cloudflare Pages with Functions
- **Desktop**: Electron with auto-updates

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting PRs.

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Credits

- Built by the bolt.gives team
- Original project: bolt.diy by StackBlitz