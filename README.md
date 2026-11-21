# MangaCut Studio V12.4

Arquivo histórico do MangaCut Studio V12.4.

---

## Descrição

O **MangaCut Studio V12.4** é uma ferramenta de edição de imagens e mangá, focada em ferramentas de transformação geométrica e integração com modelos de segmentação de anime via inteligência artificial. Este repositório serve como arquivo histórico do projeto.

---

## Status da Versão V12.4

**Versão:** V12.4 — **Transform Tools Fix**  
**Status:** Estável

### Resumo

- Correção das ferramentas de transformação geométrica (rotação, escalonamento, espelhamento, distorção).
- Integração com **SkyTNT Anime Segmentation / ISNet** via ONNX Runtime e FastAPI.
- Processamento de arquivos PSD com suporte a camadas e grupos.
- Pipeline de testes com 54 arquivos PSD.

---

## Navegação por Documentação

| Seção | Descrição |
|-------|-----------|
| [01-PROJETO](01-PROJETO/README.md) | Visão geral do projeto, status V12.4, créditos e limitações |
| [02-DOCUMENTACAO](02-DOCUMENTACAO/README.md) | Histórico de versões, funcionalidades, limitações e pendências |
| [03-ACERVO-PSD](03-ACERVO-PSD/README.md) | Inventário e status do acervo de arquivos PSD (54 arquivos) |
| [04-IA](04-IA/README.md) | Notas sobre modelos de IA, segmentação e treinamento |
| [05-RELEASES](05-RELEASES/README.md) | Histórico de lançamentos e notas de versão |

---

## Testes

### Resultados de Testes (V12.4)

| Teste | Resultado |
|-------|-----------|
| Sintaxe de 5 scripts | ✅ PASS |
| Transformação geométrica | ✅ PASS |
| Fixture PSD com 1501 camadas e 2 grupos | ✅ PASS |
| Fixture Grayscale | ✅ PASS |
| 54 imports de PSD | ✅ PASS |
| 5 round-trips individuais | ✅ PASS |
| Teste interativo completo no navegador | ❌ NÃO EXECUTADO |

---

## Limitações Conhecidas

- **Máscaras independentes do PSD:** O escritor de PSD não preserva completamente as máscaras independentes por camada.
- **Pixels fora do canvas:** Pixels fora dos limites do canvas podem ser recortados durante o processamento.
- **Memória por camada:** Necessário trabalho de alta prioridade para full-canvas-per-layer.
- **Modos de mesclagem:** Suporte limitado a blend modes de grupo, pass-through e ICC/unknown.

---

## Trabalho de Alta Prioridade

1. Memória por camada (full-canvas-per-layer)
2. Blend modes de grupo e pass-through
3. Canais/ICC/metadata de PSD
4. Modos de mesclagem desconhecidos

---

## Status do Acervo PSD

- **54 PSDs:** Arquivo de teste PSD, **não** um conjunto de dados supervisionado.
- **3 arquivos ZIP do acervo PSD:** Não estão presentes no repositório. Apenas artefatos de inventário e checksum existem.

---

## Status de Treinamento de IA

- **Modelo integrado:** SkyTNT Anime Segmentation / ISNet via ONNX Runtime e FastAPI.
- **Treinamento/Fine-tuning:** **Nenhum treinamento ou fine-tuning foi executado.** Os modelos são utilizados em seu estado original (zero-shot).
- Consulte [AI_STATUS_E_TREINAMENTO.md](AI_STATUS_E_TREINAMENTO.md) para mais detalhes.

---

## Notas sobre os 39 Painéis de Referência

- Os **39 painéis de referência** não são máscaras anotadas — são painéis de referência de imagem.

---

## Créditos

- **Projeto por:** [@edymbk](https://github.com/edymbk)
- **Documentação e assistência em IA:** E.D.I.T.H. (assistente de IA de edymbk)

Os créditos de dependências de terceiros e licenças devem ser preservados conforme os arquivos originais do projeto.

---

## Arquivos Raiz

| Arquivo | Descrição |
|---------|-----------|
| [README.md](README.md) | Visão geral do projeto (este arquivo) |
| [README_ENVIO_CODEX.md](README_ENVIO_CODEX.md) | Notas de envio para Codex |
| [MangaCut_Codex_Handoff_Completo.md](MangaCut_Codex_Handoff_Completo.md) | Documentação de handoff para Codex |
| [AI_STATUS_E_TREINAMENTO.md](AI_STATUS_E_TREINAMENTO.md) | Status de treinamento de modelos de IA |
| [CHECKSUMS_SHA256.txt](CHECKSUMS_SHA256.txt) | Somas de verificação SHA-256 dos artefatos |
| [PSD_54_INVENTARIO.csv](PSD_54_INVENTARIO.csv) | Inventário CSV dos 54 arquivos PSD |
| [PSD_54_MANIFEST_SHA256.json](PSD_54_MANIFEST_SHA256.json) | Manifesto JSON com checksums dos PSDs |
| [MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip](MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip) | ZIP das correções de Transform Tools |
