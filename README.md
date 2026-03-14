# WPBrasil Eventos

WPBrasil Eventos é uma maneira simples de pegar os eventos atuais da comunidade WordPress do Brasil.

## Como funciona

- O arquivo `AGENTS.md` centraliza todas as instruções (fontes, regras e formato).
- O comando `./get-meetups` executa `codex exec` usando esse arquivo.
- A saída final é gerada em `events.md`.

## Uso

```bash
./get-meetups
```

Por padrão, o comando mostra os detalhes da execução.

Modo silencioso:

```bash
./get-meetups --quiet
```

Stream detalhado do Codex:

```bash
./get-meetups --steps
```

## Pré-requisito

```bash
codex login
```

## Estrutura do projeto

- `AGENTS.md`
- `get-meetups`
- `LICENSE`
- `.gitignore`
