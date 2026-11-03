# Notas de trabalho: sapatas

App web estático (um único `index.html`) com as calculadoras e o leitor da referência. Veja o `README.md` para o que ele faz.

## Como o `index.html` é organizado

Tudo está em um arquivo, em blocos `<script>` na ordem abaixo (cada módulo começa com um comentário `/* src/arquivo.js */`):

- `window.REFTEXT`: texto da referência por página (`toc`, `pages`, `refs`). É JSON em uma linha; o caractere `<` vai escapado como `\u003c`. Ao regravar, mantenha esse formato.
- `window.FIGPAGES`: páginas que têm figura (`f` = número do arquivo, `file`, `page` = página do texto, `figs` = número e legenda).
- `src/data.js` (tabelas do Anexo A), `src/core.js` (formatação, memória de cálculo, materiais), `src/eng_common.js`, `src/eng_isolada.js` (sapata isolada), `src/eng_excentrica.js`, `src/eng_flex.js` (sapata flexível), `src/eng_div.js` (divisa, corrida e associada), `src/registry.js` (páginas, campos de entrada e exemplos), `src/validation.js` (conferências) e a interface no último bloco (`/* ===== INTERFACE ===== */`).
- Na interface, `NAV` define o menu, `TOCMAP` liga o sumário da referência às calculadoras, `FIGGROUP` agrupa as figuras e `FIGREL` liga cada calculadora às suas figuras.

## Imagens da referência

`figs/pNNN.jpg`: NNN = página do PDF; página do texto = NNN − 4 (001 a 004 = capa e sumário, página 0). Salve em JPG, ~1241×1755 px, qualidade ~72, progressivo. O leitor lista todas as páginas de `REFTEXT.pages`.

## Prints do README

`docs/prints/*.jpg` são gerados por `tools/prints.py` (ver o topo do script para instalar KaTeX e as fontes via npm). Refaça os prints quando mudar a aparência ou os números de uma tela mostrada no README e confira as imagens antes do commit.

## Ao mexer no código

- A página **Validação** tem de continuar toda conferida (Exemplos 1 a 9). Se mudar uma fórmula, confira o motivo antes de mexer nas tolerâncias.
- Rode `python3 tests/smoke.py` antes de cada commit (`CHROMIUM_PATH=/caminho/do/chromium` se precisar).
- Sem internet, KaTeX não carrega: as fórmulas aparecem em TeX cru, mas o texto dos resultados serve para comparar antes e depois de uma mudança.
- Mantenha a numeração dos itens e das equações igual à do texto de Bastos (2023).

## Commits

- Mensagens em português: título curto e, no corpo, o que mudou e por quê.
- Atualize o `CHANGELOG.md` no mesmo commit.
- Envie com `git push origin main`.
