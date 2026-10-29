# Use this model → llamay

Hugging Face builds the **Use this model** menu on every model page from one file,
[`packages/tasks/src/local-apps.ts`](https://github.com/huggingface/huggingface.js/blob/main/packages/tasks/src/local-apps.ts).
[`local-apps.patch`](local-apps.patch) adds llamay to it, next to Ollama, and adds a test in
`local-apps.spec.ts`.

On a GGUF model page the entry would show:

```sh
# Download llamay from https://llamay.com/download/
llamay run -m hf.co/<owner>/<repo>:<QUANT> -chat -p "Hello!"
llamay serve -m hf.co/<owner>/<repo>:<QUANT>
```

The Hub fills in `<QUANT>` from the file the visitor picked.

## Apply and test it

The patch is made against huggingface.js `e7a7d2a`.

```sh
git clone https://github.com/huggingface/huggingface.js && cd huggingface.js
git apply ../llamay-hf/huggingface-js/local-apps.patch
pnpm install
cd packages/tasks
pnpm exec vitest run src/local-apps.spec.ts
pnpm run check && pnpm run lint:check && pnpm run format:check
```

## Submit it

Open a pull request on `huggingface/huggingface.js` titled
`[Local apps] Add llamay`. The Hugging Face team reviews and merges these.
