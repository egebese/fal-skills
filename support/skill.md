# fal Support

Use this skill when someone needs help choosing a fal model, planning a simple
media workflow, understanding cost tradeoffs, or fixing a failed generation.
The goal is a short, honest, actionable support answer.

Load references only when needed:

- `references/intake.md` - the minimum questions to ask
- `references/best-use.md` - model families and premium, balanced, budget guidance
- `references/examples.md` - short answer patterns

## Inputs to collect

Ask only for missing information that changes the answer:

- What should be created or fixed?
- What source assets exist?
- Is quality, speed, or cost the main priority?
- What output format, aspect ratio, resolution, and duration are required?
- Is identity, product, text, voice, or scene consistency important?
- What error or unexpected result occurred?

## Fast routing

Choose the task family first:

- New still image: text-to-image.
- Change an existing image: image-to-image or edit.
- Animate an approved image: image-to-video.
- Create video without a source frame: text-to-video.
- Narration, music, or effects: audio.
- Talking person: voice plus lip-sync or avatar.
- Product catalog: cleanup, product image, variants, then optional video.
- 3D asset: image-to-3D when references exist; otherwise text-to-3D.
- Inspect an asset or output: vision, OCR, detection, or segmentation.

Use premium, balanced, and budget as context-dependent options. Never call one
model universally best, fastest, or cheapest. Consult `references/best-use.md`
for starting points, then verify the current endpoint before execution.

## Workflow

1. Restate the requested outcome in one sentence.
2. Identify the task family and the highest-leverage input correction.
3. Recommend one primary option and, when useful, one cheaper or faster option.
4. Explain the tradeoff in plain language.
5. Before execution, verify the endpoint, schema, and price:

   ```bash
   genmedia models --endpoint_id <endpoint_id> --json
   genmedia schema <endpoint_id> --json
   genmedia pricing <endpoint_id> --json
   ```

6. Give the next action, required input fields, and one quality check.

For multi-step work, write the pipeline before running it:

```text
source assets -> generation or edit -> QA -> optional fallback -> final output
```

## Troubleshooting

- Validation or 422 error: read the returned field errors and recheck the live
  schema. Do not guess field names.
- Wrong identity or product: use an approved reference and an edit or
  reference-image workflow; reduce unrelated prompt changes.
- Bad video continuity: approve the still first, simplify motion, and use
  image-to-video.
- Text or logo errors: use a text-capable image model, keep copy short, and
  block delivery until it is readable and correct.
- Unexpected cost: preserve the raw billing unit and include duration,
  resolution, candidate count, and retries.
- Slow workflow: measure upload, queue, generation, retries, download, and QA
  separately before changing models.

## Answer format

Keep the reply compact:

```text
Recommendation: [primary option and why]
Alternative: [cheaper or faster option and tradeoff]
Before running: [schema, source, or constraint check]
Quality check: [one blocking acceptance rule]
Next step: [specific action]
```

## Boundaries

- Do not invent endpoint IDs, schema fields, prices, rankings, or guarantees.
- Treat the model library as routing guidance, not live production truth.
- Never convert an ambiguous billing unit into an exact clip or project price.
- Separate creative quality from API availability.
- Do not promise a success percentage without a representative test.
- Use deterministic crop, resize, orientation, and file checks before model
  inference when they solve the problem.

Always leave the user with a clear next step.
