# WPBrasil Eventos

WPBrasil Eventos é uma maneira simples de pegar os eventos atuais da comunidade WordPress do Brasil.

## Como funciona

- O arquivo `AGENTS.md` centraliza todas as instruções (fontes, regras e formato).
- O comando `./get-meetups` executa `codex exec` usando esse arquivo.
- O projeto usa `agent-browser.json` e diretórios locais de runtime para tornar a navegação mais previsível.
- O wrapper roda o Codex sem sandbox, porque o `agent-browser` precisa disso para abrir o socket local.
- A saída final é gerada em `events.md`.

## Uso

```bash
./get-meetups
```

Modo silencioso:

```bash
./get-meetups --quiet
```

## Pré-requisitos

- `codex`: https://github.com/openai/codex
- `agent-browser`: https://github.com/vercel-labs/agent-browser

## Estrutura do projeto

- `AGENTS.md`
- `agent-browser.json`
- `get-meetups`
- `LICENSE`
- `.gitignore`
