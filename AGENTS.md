# Meetup Markdown Agent

## Goal
Generate `events.md` with Meetup events using the rules below.

## Source Pages
Use exactly these Meetup pages as sources:

- https://www.meetup.com/pt-BR/wpcuritiba/events/
- https://www.meetup.com/pt-BR/wp-poa/events/
- https://www.meetup.com/pt-BR/WordPressBeloHorizonte/events/
- https://www.meetup.com/pt-BR/wpsampa/events/
- https://www.meetup.com/pt-BR/Meetup-WordPress-Floripa/events/
- https://www.meetup.com/pt-BR/wpfortaleza/events/
- https://www.meetup.com/wp-rio/events/
- https://www.meetup.com/pt-BR/barueri-wordpress-meetup/events/

## Output File
Write final output to `events.md`.

## Output Format
Use one line per event with this exact template:

`{date_pt} – **[{title}]({url})**, organizada pela comunidade {community_phrase}.`

## Data Rules
- Only include events that belong to each source group page (ignore recommended/similar events from other groups).
- Include only upcoming events: event date must be on the command run date (today) or after it, in local timezone.
- Exclude any past event.
- If event date is missing or ambiguous, exclude the event.
- Sort by date ascending.
- Deduplicate by event URL.
- Use Portuguese month abbreviations in `date_pt`: JAN, FEV, MAR, ABR, MAI, JUN, JUL, AGO, SET, OUT, NOV, DEZ.
- Use proper Portuguese grammar for community phrase (`de`/`do`), e.g. `do **Rio de Janeiro**`.

## Talk Aggregation Rules
- If an event has multiple talks in its content, combine them into one title:
`Palestras presenciais "TALK 1" (com SPEAKER 1) e "TALK 2" (com SPEAKER 2)`
- Apply this when talk titles/speakers are available in the event content.

## Final Response
- Print the generated markdown in the terminal output too.
- Also print a short summary with number of events written.
