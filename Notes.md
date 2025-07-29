# Notes

These are my notes.

I didn't like the rendering of equations with Mathjax, so I added the following so that it's rendered with Katex instead (same renderer as in VSCode apparently):
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css" integrity="sha384-n8MVd4RsNIU0tAv4ct0nTaAbDJwPJzDEaqSD1odI+WdtXRGWt2kTvGFasHpSy3SV" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js" integrity="sha384-XjKyOOlGwcjNTAIQHIpgOno0Hl1YQqzUOEleOLALmuqehneUG+vnGctmUb0ZY0l8" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/contrib/auto-render.min.js" integrity="sha384-+VBxd3r6XgURycqtZ117nYw44OOcIax56Z4dCRWbxyPt0Koah1uHoK0o4+/RRE05" crossorigin="anonymous"
        onload="renderMathInElement(document.body, {
          delimiters: [
            {left: '$$', right: '$$', display: true},
            {left: '$', right: '$', display: false},
            {left: '\\[', right: '\\]', display: true},
            {left: '\\(', right: '\\)', display: false}
          ]
        });"></script>
```
(thanks ChatGPT)

Regarding the rendering of equations in `<details>` sections, there are two options:
- Either keep `<details>` as is, in which case the content is parsed as HTML (not markdown), so line breaks should be indicated with `<br/>` etc (HTML syntax)
- Or, write `<details markdown="1">` so that content is parsed as Markdown, but for some reasons column vectors are f*cked up: line breaks `\\` are interpreted as escaped `\`, so they should be doubled instead: `\\\\`
  - Update: actually, writing `$$ ... $$` (with double dollar sign) does the trick. There is no new line unless a double line break is added in markdown.



Idea: for collapsible sections in details tag, maybe add emojis like ℹ️ to indicate interesting precisions, off-topic comment and details of computations?

Use Yann LeCac as a Twitter handle

Should I buy machinelearningforlegends.com? 

Em dash: —

Ideas of improvements:
Banner image (that shrinks to persisent header when scrolling)
Possibility to change language?
Better preview of posts: image, start of text
+ Group by categories