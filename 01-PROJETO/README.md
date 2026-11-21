# 01-PROJETO: Visão Geral do Projeto

## MangaCut Studio V12.4

**Status:** Estável — Transform Tools Fix

O **MangaCut Studio V12.4** é uma ferramenta de edição de imagens e mangá focada em ferramentas de transformação geométrica aprimoradas, integração com segmentação de anime via IA e processamento de arquivos PSD.

---

## Status da Versão V12.4

Esta versão foca na correção das ferramentas de transformação geométrica (rotação, escalonamento, distorção) e inclui integração com modelos de segmentação de anime via ONNX Runtime.

### Principais Mudanças em V12.4

- Correção das ferramentas de transformação (rotação, escalonamento, espelhamento).
- Integração com segmentação de anime via SkyTNT Anime Segmentation / ISNet.
- Processamento de arquivos PSD com suporte a camadas e grupos.
- Pipeline de teste expandido com verificação de 54 arquivos PSD.

---

## Navegação

| Seção | Descrição |
|-------|-----------|
| [02-DOCUMENTACAO](../02-DOCUMENTACAO/README.md) | Histórico de versões, funcionalidades, limitações e pendências |
| [03-ACERVO-PSD](../03-ACERVO-PSD/README.md) | Inventário e status do acervo de arquivos PSD |
| [04-IA](../04-IA/README.md) | Notas sobre modelos de IA, treinamento e segmentação |
| [05-RELEASES](../05-RELEASES/README.md) | Histórico de lançamentos e notas de versão |

---

## Arquivos Raiz

| Arquivo | Descrição |
|---------|-----------|
| [README.md](../README.md) | Visão geral do projeto (arquivo raiz) |
| [README_ENVIO_CODEX.md](../README_ENVIO_CODEX.md) | Notas de envio para Codex |
| [MangaCut_Codex_Handoff_Completo.md](../MangaCut_Codex_Handoff_Completo.md) | Documentação de handoff para Codex |
| [AI_STATUS_E_TREINAMENTO.md](../AI_STATUS_E_TREINAMENTO.md) | Status do treinamento de modelos de IA |
| [CHECKSUMS_SHA256.txt](../CHECKSUMS_SHA256.txt) | Somas de verificação SHA-256 dos artefatos |
| [PSD_54_INVENTARIO.csv](../PSD_54_INVENTARIO.csv) | Inventário CSV dos 54 arquivos PSD |
| [PSD_54_MANIFEST_SHA256.json](../PSD_54_MANIFEST_SHA256.json) | Manifesto JSON com checksums dos PSDs |

---

## Limitações Conhecidas

- **Máscaras independentes no PSD:** O escritor de PSD não preserva completamente as máscaras independentes por camada.
- **Pixels fora do canvas:** Pixels fora dos limites do canvas podem ser recortados durante o processamento.
- **Memória por camada:** Trabalho de alta prioridade necessário para processamento de canvas completo por camada.
- **Modos de mesclagem:** Suporte limitado a modos de mesclagem de grupo, pass-through e ICC.

---

## Créditos

- **Projeto desenvolvido por:** [@edymbk](https://github.com/edymbk)
- **Documentação e assistência em IA:** E.D.I.T.H. (assistente de IA de edymbk)

Os créditos de dependências de terceiros devem ser mantidos conforme os arquivos de licença originais do projeto.
