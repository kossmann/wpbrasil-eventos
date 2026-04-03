# WPBrasil Eventos Agent

## Objective
Generate `events.md` with current/future Meetup events from WordPress communities in Brazil.

## Mandatory Tool
- Use `agent-browser` to open and navigate Meetup pages.
- Avoid generic web search when `agent-browser` can do it.
- Do not use `curl` or other fallback scraping tools.
- If `agent-browser` is blocked or unavailable, stop immediately and report that in one line.
- Work directly from the listed source pages and their event detail pages only.
- Keep the run short: do not explore unrelated pages, do not retry the same extraction approach many times, and skip a source page if it clearly has no future events.
- Reference: https://github.com/vercel-labs/agent-browser
- Preferred flow:
  - `agent-browser open <url>`
  - `agent-browser wait <ms>`
  - `agent-browser snapshot -i -c`
  - `agent-browser get text ...`
  - `agent-browser get attr href ...`

## Source Pages
- https://www.meetup.com/pt-BR/wpcuritiba/events/
- https://www.meetup.com/pt-BR/wp-poa/events/
- https://www.meetup.com/pt-BR/WordPressBeloHorizonte/events/
- https://www.meetup.com/pt-BR/wpsampa/events/
- https://www.meetup.com/pt-BR/Meetup-WordPress-Floripa/events/
- https://www.meetup.com/pt-BR/wpfortaleza/events/
- https://www.meetup.com/wp-rio/events/
- https://www.meetup.com/pt-BR/barueri-wordpress-meetup/events/

## Output
- File: `events.md`
- One line per event:
  - `{date_pt} – **[{title}]({url})**, {organized_word} pela comunidade {community_phrase}.`

## Rules
- Recommended execution order:
  - Open one source page.
  - Capture the visible future event cards from that page only.
  - Collect only candidate event URLs that belong to the same source group.
  - Skip the source page immediately if there are no future events.
  - Open each candidate event URL once to extract the final data.
- Include only events from the source group itself.
- Ignore recommended/similar events from other groups.
- Include only events on/after today (local timezone).
- Exclude events with missing/ambiguous date.
- Sort ascending by date.
- Deduplicate by URL.
- Prefer the minimum number of browser actions needed to finish.
- Do not re-open the same listing page or event page unless a previous read clearly failed.
- `date_pt` format: `DAY.MONTH`, for example `28.MAR`.
- `date_pt` months: `JAN FEV MAR ABR MAI JUN JUL AGO SET OUT NOV DEZ`.
- Use correct grammar for community phrase (`de`/`do`), e.g. `do **Rio de Janeiro**`.
- Determine `{title}` from the event content, not from the Meetup page title alone.
- Keep a specific title only when the event page clearly identifies an actual subject or named activity, such as a talk, workshop, panel, roundtable, office hours, or another concrete agenda item.
- If there is no clear subject or named activity in the event content, do not keep or paraphrase the original Meetup title. Replace it with a generic attendance label instead.
- Treat titles as generic when they mainly identify the community meeting itself, date/month, edition number, city, or group name, without a clear subject or activity.
- The Meetup page title by itself is not enough to justify keeping a specific title.
- Decision rule for every event:
  - If the page includes a named talk, workshop, panel, roundtable, or other concrete subject, use that subject to build the title.
  - Otherwise, use `Evento presencial` or `Evento online`.
- Replace generic titles with:
  - `Evento presencial` for in-person events.
  - `Evento online` for online events.
- Use `organizado` when the chosen title starts with `Evento`.
- Use `organizada` for other titles, including multi-talk titles.

## Multi-talk Events
- If an event has multiple talks, combine as:
  - `Palestras presenciais "TALK 1" (com SPEAKER 1) e "TALK 2" (com SPEAKER 2)`

## Final Response
- Print the generated markdown.
- Print a short summary with total events written.
