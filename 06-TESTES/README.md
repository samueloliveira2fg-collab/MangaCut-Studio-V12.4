# MangaCut Studio V12.4 — 06-TESTES

Este diretório documenta os testes do projeto MangaCut Studio V12.4.

## Tabela de testes

| Teste | Resultado |
|-------|-----------|
| Sintaxe: 5 scripts | PASS |
| Transform geometry | PASS |
| PSD fixture sintética (1501 camadas / 2 grupos) | PASS |
| Fixture Grayscale | PASS |
| Imports: 54 PSDs | PASS |
| 5 round-trips individuais | PASS |
| Teste interativo completo no browser | NÃO EXECUTADO |

## Observações sobre testes

- **Pass no import ≠ pass no round-trip.** Apenas 5 dos 54 PSDs passaram no teste de ida e volta.
- Os PSDs são **ativos de teste**, não dados de treinamento supervisionado.

## Links de referência

- [`../PSD_54_INVENTARIO.csv`](../PSD_54_INVENTARIO.csv)
- [`../PSD_54_MANIFEST_SHA256.json`](../PSD_54_MANIFEST_SHA256.json)
- [`../MangaCut_Codex_Handoff_Completo.md`](../MangaCut_Codex_Handoff_Completo.md)

## Arquivos ausentes

As **partes faltantes do arquivo PSD** bloqueiam a reprodução do corpus completo.

## Créditos

- **@edymbk**
- **E.D.I.T.H.**
