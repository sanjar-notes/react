# 20. getByLabelText
Created Mon Sep 30, 2024 at 10:08 AM

## input.correspondingLabel.textContent
- Works on text of the `label` for an `input` (i.e. `id` and `htmlFor` match)
- Works for label-embedded input as too, i.e. RTL will ignore the input tag, and only read textContent.

## options
- `selector` - htmlTagName will further narrow down search to only that type of HTML element (if multiple labels with the same text are present). btw, this is a rare occurrence (i.e. two labels with the same text).