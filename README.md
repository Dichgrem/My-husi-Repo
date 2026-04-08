> Automatically tracks [Husi](https://codeberg.org/xchacha20-poly1305/husi) upstream releases, checks daily and publishes as a ready-to-use pacman repository via GitHub Pages.
> 
> *Husi: A non-professional and recreational proxy tool integration.*

## Usage

Add to the end of `/etc/pacman.conf`:

```ini
[husi]
SigLevel = Optional TrustAll
Server = https://Dichgrem.github.io/My-husi-Repo/x86_64
```

Then install:

```bash
sudo pacman -Sy
sudo pacman -S fr.husi
```

> **Note**: Husi requires Java 21 or higher. It is recommended to install `jdk21-openjdk` or `jre21-openjdk`.

## How to fork

1. Fork this repository
2. Go to Settings → Pages, set Build and deployment Source to **Deploy from a branch**, and Branch to **gh-pages** (root)
3. Go to Settings → Actions → General, set Workflow permissions to **Read and write permissions**
4. Manually trigger the workflow: Actions → Build & Publish Arch Repo → Run workflow
5. Once the build completes, verify at `https://<your-username>.github.io/<repo-name>/`

## How it works

```
Every day at UTC 06:00
    ↓
Fetch latest upstream version via Codeberg API
    ↓
Compare with version.txt — skip if unchanged
    ↓
In an Arch Linux container: Download upstream pre-built .pkg.tar.zst
    ↓
Generate pacman database with repo-add
    ↓
Deploy to gh-pages, keeping only the latest package
```