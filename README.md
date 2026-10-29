# llamay-hf

Run any GGUF model on the Hugging Face Hub with [llamay](https://llamay.com), and the
pieces that put llamay on Hugging Face itself.

## Run a Hugging Face model

llamay reads a Hub repository directly. The tag after the colon picks the quantisation:

```sh
llamay run -m hf.co/bartowski/SmolLM2-135M-Instruct-GGUF:Q4_K_M -chat -p "Hello!"
```

The first run downloads the file, checks its sha256 and stores it; later runs start at once.
To serve it to other apps instead:

```sh
llamay serve -m hf.co/bartowski/SmolLM2-135M-Instruct-GGUF:Q4_K_M
```

That serves OpenAI-compatible (`/v1/chat/completions`) and Anthropic-compatible
(`/v1/messages`) routes on `127.0.0.1`. Ask for the model by its full name,
`hf.co/<owner>/<repo>:<quant>`.

| Reference | Meaning |
|---|---|
| `hf.co/<owner>/<repo>:<quant>` | a quantisation in that repository, such as `Q4_K_M` or `Q8_0` |
| `hf:<owner>/<repo>/<file.gguf>[@rev]` | one exact file, optionally at a revision |

For a gated repository, set `HF_TOKEN` and llamay sends it with requests to Hugging Face.

Both commands need llamay 0.4.13 or later. Download it from
[llamay.com/download](https://llamay.com/download/).

## In this repository

| Path | What it is |
|---|---|
| [`huggingface-js/`](huggingface-js/) | The entry that adds llamay to the **Use this model** menu on GGUF model pages, as a patch to [`huggingface/huggingface.js`](https://github.com/huggingface/huggingface.js) |
| [`hf-org-card/`](hf-org-card/) | The README card and logo for llamay's organization page on the Hub |

## Status

- [x] `hf.co/...` references work in `llamay run` and `llamay serve` (tested with 0.4.13)
- [ ] Organization page on huggingface.co
- [ ] Local-apps entry proposed upstream in huggingface.js

## Licence

The contents of this repository are Apache-2.0, the same licence as huggingface.js.
llamay itself is a separate product of Kosa8 Labs under its own licence.
