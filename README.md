# PowerAI Hub — Colab launchers

One Colab notebook per primitive published on [PowerAI Hub](https://hub.powerai.ai).
Each notebook fetches that primitive's published archive from the Hub's public API
and unpacks it into your Colab session, so you can run it on Google's hardware
without installing anything.

You do not need this repo to use the Hub. It exists because **Colab only opens
notebooks from a public GitHub repo, a gist, or Drive** — never from an arbitrary
URL — so the Hub cannot serve a notebook and link straight to it. The "Run in Colab"
button on a primitive page points here.

## Using one

Open a primitive on the Hub and press **Run in Colab**, or open a notebook here and
click the Colab badge. Then **Runtime → Run all** (⌘/Ctrl + F9) — Colab does not
auto-run a notebook opened from a URL, by design.

The first cell clears `/content/primitive`, downloads the archive, and unpacks it, so
re-running is always a clean start.

## What these notebooks are not

- **Not the Hub running your code.** The Hub executes nothing. Everything here runs
  in your own Colab session, under your Google account, on Google's free tier.
- **Not upstream's latest commit.** A notebook fetches the *published version*
  recorded on the Hub, which is a snapshot and may lag the origin repository.
- **Not authenticated.** These notebooks carry no tokens and need none; the archive
  endpoint they call is public. Never add a credential to a notebook here — this repo
  is public.

## Regenerating

Generated from the Hub's public catalogue, not by hand. From the `powerai-hub`
checkout:

```bash
cd apps/api
uv run python manage.py render_colab_launchers --out ../../powerai-launcher --from-api
```

`--from-api` reads the live catalogue at `https://hub-api.powerai.ai`, so the set here
matches what is actually published. Re-run it after new primitives land: a primitive
with no notebook has a Run in Colab button that 404s.
