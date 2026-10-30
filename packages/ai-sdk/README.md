# @openai-oauth/ai-sdk

[CLI docs](../../README.md) | [npm](https://www.npmjs.com/package/@openai-oauth/ai-sdk)

Connect OpenAI OAuth credentials to the Vercel AI SDK.

```bash
npm i @openai-oauth/ai-sdk @openai-oauth/local ai
```

Quickstart:

```ts
import { createOpenAIOAuth } from "@openai-oauth/ai-sdk";
import { openaiCredentials } from "@openai-oauth/local";
import { generateText } from "ai";

const openai = createOpenAIOAuth(openaiCredentials());

const result = await generateText({
	model: openai("gpt-5.4-mini"),
	prompt: "Hello!",
});
```

Generate or edit images with GPT Image 2:

```ts
import { readFile } from "node:fs/promises";
import { generateImage } from "ai";

const result = await generateImage({
	model: openai.image("gpt-image-2"),
	prompt: "A tiny house in a forest",
});

const inputImage = await readFile("input.png");
const edited = await generateImage({
	model: openai.image("gpt-image-2"),
	prompt: {
		text: "Add a red hat",
		images: [inputImage],
	},
});
```

## Package Notes

`@openai-oauth/ai-sdk` accepts any OpenAI OAuth credential source.

Use local credentials on your own machine:

```ts
import { openaiCredentials } from "@openai-oauth/local";

const openai = createOpenAIOAuth(openaiCredentials());
```

API shape:

```ts
const openai = createOpenAIOAuth(credentials);

openai("gpt-5.4-mini");
openai.languageModel("gpt-5.4-mini");
openai.image("gpt-image-2");
openai.imageModel("gpt-image-2");
```

Exports:

- `createOpenAIOAuth`
- `OpenAIOAuthProvider`
- `OpenAIOAuthProviderInput`
- `OpenAIOAuthProviderSettings`
- `OpenAIOAuthModelId`
- `OpenAIOAuthImageModelId`

## More

See the [proxy CLI documentation](../../README.md) for running the local OpenAI-compatible server.
