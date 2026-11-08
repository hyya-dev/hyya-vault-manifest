# hyya-vault-manifest — the signed list of on-device models in hYYa ai

This repository publishes the list of models that **hYYa Vault**, the on-device engine of
**[hYYa ai](https://hyya.com/hyya-ai.html)**, offers to download. It is public so anyone can see exactly
what the app offers and check that the list is the one we signed.

- **[hYYa ai — download and details](https://hyya.com/hyya-ai.html)**
- **[hYYa ai docs, FAQ and issue tracker](https://github.com/hyya-dev/hyya-ai-docs)**

## What is in it

| File | What it is |
|---|---|
| `models.json` | The catalogue: each model's name, where its files are hosted, which devices it suits, and the memory it needs. It holds **no model weights** — those download from their public host, only when you choose a model. |
| `models.json.minisig` | A [minisign](https://jedisct1.github.io/minisign/) signature over `models.json`. |

The app ships with a copy of this list built in, so it works offline from the first launch. When you tap
**Check for new models**, it fetches the published copy from
`https://hyya-dev.github.io/hyya-vault-manifest/` and uses it only if:

1. the signature checks out against the public key built into the app (Ed25519 over a BLAKE2b-512 digest of
   the file — minisign's hashed mode), and
2. the list is newer than the one the app already has.

If either check fails, the app keeps the list it has. A model you download is checked again on its own: its
files must match the size and SHA-256 checksum their host publishes before the app calls the model installed.

## Check the signature yourself

The public key the app carries:

```
untrusted comment: minisign public key 1C7D9CADDBA3C5A9
RWSpxaPbrZx9HAooZcr/bcizeo4SBoXnseMSUrttopMJYUl3Yeko5oTA
```

With [minisign](https://jedisct1.github.io/minisign/) installed:

```
minisign -Vm models.json -P RWSpxaPbrZx9HAooZcr/bcizeo4SBoXnseMSUrttopMJYUl3Yeko5oTA
```

`Signature and comment signature verified` means the file is exactly the one we published.

## Which models

Open models from the Qwen, Gemma and Llama families for chat; small search models (E5 and BGE families)
that let DataLens find passages in your documents; and Stable Diffusion models that illustrate exported decks
and documents on Mac and iPad. Each is listed with the devices it suits. A person decides what enters the list —
nothing is added automatically.
