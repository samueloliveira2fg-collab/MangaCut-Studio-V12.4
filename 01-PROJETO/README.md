# 01-PROJETO: Visão Geral do Projeto

## MangaCut Studio V12.4

**Status:** Estável — Transform Tools Fix

---

## Descrição

O **MangaCut Studio V12.4** é uma ferramenta de edição de imagens e mangá focada em ferramentas de transformação geométrica aprimoradas, integração com segmentação de anime via IA e processamento de arquivos PSD.

**Versão:** V12.4 — Transform Tools Fix

Este repositório é um arquivo histórico do projeto.

---

## Navegação

- [02-DOCUMENTACAO](../02-DOCUMENTACAO/README.md)
- [03-ACERVO-PSD](../03-ACERVO-PSD/README.md)
- [04-REFERENCIAS](../04-REFERENCIAS/README.md)
- [05-CODIGO-FONTE](../05-CODIGO-FONTE/README.md)
- [06-TESTES](../06-TESTES/README.md)

---

## Arquivo ZIP Principal

O ZIP principal permanece na raiz do repositório:
[MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip](../MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip)

---

## Versão V12.4 — Transform Tools Fix

- Correção das ferramentas de transformação geométrica (rotação, escalonamento, espelhamento).
- Integração com **SkyTNT Anime Segmentation / ISNet** via ONNX Runtime e FastAPI.
- Processamento de arquivos PSD com suporte a camadas e grupos.

---

## Limitações Conhecidas

- **Máscaras independentes no PSD:** O escritor de PSD não preserva completamente as máscaras independentes por camada.
- Pixels fora da área da tela podem ser recortados.
- Nenhum treinamento de IA foi realizado.

---

## Créditos

Projeto @edymbk. Documentação e assistência por **E.D.I.T.H.**
