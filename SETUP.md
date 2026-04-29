# Private Code → Public Releases Setup

## Architecture

```
┌─────────────────────┐          ┌──────────────────────────┐
│  agentic (PRIVATE)  │  ──▶    │  agentic-model (PUBLIC)   │
│                     │          │                          │
│  All source code    │  tag    │  README.md              │
│  Build pipeline     │  push   │  GitHub Releases page    │
│  License logic      │  v3.x   │  Binary downloads       │
│  Self-healing       │         │  SHA-256 checksums      │
└─────────────────────┘          └──────────────────────────┘
```

## Setup Steps

### Step 1: Public repo already exists ✅

`github.com/Vickyrrrrrr/agentic-model` — README has been pushed.

### Step 2: Create a GitHub Personal Access Token (PAT)

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Name: `agentic-release-publisher`
4. Expiration: `No expiration`
5. Scope: **`repo`** (full control of private repos)
6. Copy the token — you won't see it again

### Step 3: Add secrets to the PRIVATE repo

Go to your private `agentic` repo → Settings → Secrets and variables → Actions

Add these:

| Name | Value | Description |
|------|-------|-------------|
| `RELEASE_REPO` | `Vickyrrrrrr/agentic-model` | Owner/repo where releases go |
| `RELEASE_TOKEN` | `ghp_xxxxxxxxxxxx` | PAT from Step 2 |

### Step 4: Trigger a release

```bash
# In your private agentic repo:
git tag v3.0.5
git push --tags
```

GitHub Actions will:
1. Build Linux + macOS binaries
2. Generate SHA-256 checksums
3. Post the release + binaries to the PUBLIC `agentic-model` repo

### Step 5: Push the updated README

```bash
cd release-repo
git push origin main
```

## How users experience it

```
User visits: github.com/Vickyrrrrrr/agentic-model
  → Sees README with install instructions
  → Clicks "Releases" tab
  → Downloads agentic-linux-amd64
  → chmod +x agentic-linux-amd64
  → ./agentic-linux-amd64 login  (enters license key)
  → ./agentic-linux-amd64 build --name counter --desc "..."
```

Your private code stays private. Only the compiled binary goes public.
