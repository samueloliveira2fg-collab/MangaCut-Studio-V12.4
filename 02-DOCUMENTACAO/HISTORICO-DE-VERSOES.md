# Histórico de Versões do MangaCut Studio

Este documento registra o histórico de versões e mudanças do MangaCut Studio, com ênfase na versão atual V12.4.

---

## Versão Atual: V12.4 — Transform Tools Fix

**Status:** Estável

### Resumo das Alterações

Esta versão focou em correções das ferramentas de transformação geométrica e na integração com modelos de segmentação de anime via IA.

### Detalhamento

- **Transform Tools Fix:** Correção de bugs nas ferramentas de rotação, escalonamento, espelhamento e distorção de camadas.
- **Integração com IA:** Implementação do suporte a segmentação de anime usando SkyTNT Anime Segmentation / ISNet via ONNX Runtime e FastAPI.
- **Processamento PSD:** Melhorias na leitura de arquivos PSD com suporte a múltiplas camadas e grupos.
- **Pipeline de Testes:** Criação de testes automatizados para verificação de 54 arquivos PSD, syntax checking de scripts, e round-trips de arquivos.

---

## Histórico Anterior

### Versões Anteriores ao V12.4

O projeto MangaCut Studio evoluiu desde sua concepção por [@edymbk](https://github.com/edymbk) como uma ferramenta de edição de imagens voltada para animação de mangá. As versões anteriores focaram na base de processamento de imagens e estrutura de camadas.

> **Nota:** Detalhes das versões anteriores ao V12.4 podem ser consultados no arquivo [MangaCut_Codex_Handoff_Completo.md](../MangaCut_Codex_Handoff_Completo.md).

---

## Status de Treinamento de IA

A partir do V12.4, o projeto integra modelos de IA pré-treinados para segmentação de anime.

- **Modelo usado:** SkyTNT Anime Segmentation / ISNet
- **Formato:** ONNX Runtime
- **API:** FastAPI para inferência
- **Treinamento:** **Nenhum treinamento ou fine-tuning foi executado.** Os modelos são utilizados em seu estado original (zero-shot).
- Consulte também [AI_STATUS_E_TREINAMENTO.md](../AI_STATUS_E_TREINAMENTO.md) para mais detalhes.

---

## Notas sobre a Versão V12.4

| Aspecto | Status |
|---------|--------|
| Transform Tools | Corrigidos |
| Integração IA (ISNet) | Implementada |
| Suporte PSD (leitura) | Funcional |
| Suporte PSD (escrita) | Parcial (ver [Limitações](LIMITACOES-E-PENDENCIAS.md)) |
| Treinamento de modelos | Não realizado |
| Testes automatizados | Parciais (ver [Funcionalidades e Estado](FUNCIONALIDADES-E-ESTADO.md)) |

---

## Créditos de Documentação

- **Projeto:** [@edymbk](https://github.com/edymbk)
- **Documentação e assistência em IA:** E.D.I.T.H. (assistente de IA de edymbk)
