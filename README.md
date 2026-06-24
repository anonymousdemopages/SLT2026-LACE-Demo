# LACE — Anonymous Audio Demo

Static demo page for the SLT 2026 submission. No build step, no dependencies — just HTML/CSS/JS.

## Add your audio

Files are loaded from `<base>/<sampleId>/<methodKey>.wav`. The `base` and the method `key`s come
from the `CONFIG` block at the bottom of `index.html`. Default layout:

```
demo/audio/
├── recon_dp_rate/          # 1a. DP rate sweep (DAC backbone)
│   ├── utt1/  gt.wav
│   │          single_010.wav  lace_010.wav     # γ = 0.1
│   │          single_030.wav  lace_030.wav     # γ = 0.3
│   │          single_050.wav  lace_050.wav     # γ = 0.5
│   │          single_070.wav  lace_070.wav     # γ = 0.7
│   ├── utt2/  ...
│   └── utt3/  ...
├── recon_models/           # 1b. Compression models at a matched bitrate
│   ├── utt1/  gt.wav
│   │          dp_single.wav   dp_lace.wav
│   │          cos_single.wav  cos_lace.wav
│   │          den_single.wav  den_lace.wav
│   ├── utt2/  ...
│   └── utt3/  ...
├── recon_backbone/         # 1c. Codec backbones (DP), matched bitrate
│   ├── utt1/  gt.wav
│   │          dac_single.wav  dac_lace.wav
│   │          ss_single.wav   ss_lace.wav
│   │          enc_single.wav  enc_lace.wav
│   ├── utt2/  ...
│   └── utt3/  ...
└── tts/                    # 2. TTS configurations
    ├── tts1/  nocomp.wav
    │          single_050.wav  single_070.wav
    │          lace_050_l2.wav lace_050_l4.wav  lace_070_l2.wav
    ├── tts2/  ...
    └── tts3/  ...
```

- To add/rename **rates, models, configs, or samples**, edit only the `CONFIG` block in `index.html`.
- `groups` produce the grouped two-row column headers (e.g., a γ value spanning Single + LACE).
- Missing files just show an empty player, so you can fill them in gradually.
- Add a transcript by filling the `text` field of a sample (the Transcript column appears
  automatically when any sample in a section has text).

## Preview locally

```
cd demo
python3 -m http.server 8000     # open http://localhost:8000
```

## Deploy (private repo → anonymous mirror)

1. Push the contents of `demo/` to a **private** GitHub repo.
2. (Optional) enable GitHub Pages to test rendering.
3. Anonymize via **Anonymous GitHub** (https://anonymous.4open.science) and put the generated
   link in the paper / OpenReview.

## Anonymity checklist (before sharing)

- [ ] No author names, affiliations, or emails in `index.html` or audio file metadata.
- [ ] No personal/lab GitHub or Hugging Face links.
- [ ] Audio file names contain no identifying info.
- [ ] Scrub the git author identity so commits don't leak you:
      `git config user.name "Anonymous" && git config user.email "anon@example.com"`
