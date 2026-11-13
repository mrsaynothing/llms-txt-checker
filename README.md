# llms.txt checker

A one-file, client-side grader for [llms.txt](https://llmstxt.org/) — the
proposed standard that tells AI crawlers and answer engines what a site
actually wants them to read. Paste your file (or fetch one) and get:

- a **spec grade** (0–100) with a verdict
- per-check receipts: exactly one H1 on line 1 · a blockquote summary
  right after it · `##` sections that each carry links · link lines shaped
  `- [title](url): description`
- a **fix list** — the shortest path from your file to a passing file
- a copyable clean skeleton to rebuild from

Nothing leaves the browser: no upload endpoint, no analytics, no build
step. `index.html` is the whole tool.

## Why

The grammar is one page, and most shipped files still fail it — missing
summary blockquotes, links floating outside sections, duplicated URLs,
`http://` links. Every failure is a small tax on the machines you wrote
the file for. The checker prices that tax.

## Checks

| check | weight | why it matters |
|---|---|---|
| exactly one H1, first line | −25 fail | the spec's anchor; scrapers key on it |
| blockquote summary after H1 | −8 warn | the elevator pitch agents quote |
| at least one `##` section | −25 fail | curation is the point |
| every section has ≥1 link | −25 fail | an empty section is a dead end |
| links outside any section | −8 warn | context loss |
| `http://` links | −8 warn | mixed security |
| duplicate URLs | −8 warn | wasted crawl |
| bidi / zero-width controls | −25 fail | some ingest pipelines force-pend on them |

## Run it

Static file — open `index.html`, or serve the folder. GitHub Pages hosts
it: <https://mrsaynothing.github.io/llms-txt-checker/>

Companion write-up: *llms.txt checker — grade your file before the bots
do* on [mrsaynothing.dev](https://mrsaynothing.dev).

## License

MIT
