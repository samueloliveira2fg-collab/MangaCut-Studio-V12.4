# MangaCut Studio V12.4

Arquivo histórico do MangaCut Studio V12.4.

---

## Finalidade

Arquivo histórico público para consulta e continuação.

**Status:** V12.4 — Transform Tools Fix

---

## Arquivo ZIP Principal

O ZIP principal do projeto está atualmente na raiz do repositório:
[MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip](MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip)

---

## Navegação

- [01-PROJETO](01-PROJETO/README.md)
- [02-DOCUMENTACAO](02-DOCUMENTACAO/README.md)
- [03-ACERVO-PSD](03-ACERVO-PSD/README.md)
- [04-REFERENCIAS](04-REFERENCIAS/README.md)
- [05-CODIGO-FONTE](05-CODIGO-FONTE/README.md)
- [06-TESTES](06-TESTES/README.md)

---

## Arquivos de Suporte

- [MangaCut_Codex_Handoff_Completo.md](MangaCut_Codex_Handoff_Completo.md)
- [AI_STATUS_E_TREINAMENTO.md](AI_STATUS_E_TREINAMENTO.md)
- [PSD_54_INVENTARIO.csv](PSD_54_INVENTARIO.csv)
- [PSD_54_MANIFEST_SHA256.json](PSD_54_MANIFEST_SHA256.json)
- [CHECKSUMS_SHA256.txt](CHECKSUMS_SHA256.txt)
- [README_ENVIO_CODEX.md](README_ENVIO_CODEX.md)

---

## Matriz de Testes

- **5 scripts — sintaxe:** PASS
- **Transform geometry:** PASS
- **PSD synthetic fixture (1501 camadas / 2 grupos):** PASS
- **Grayscale fixture:** PASS
- **54 imports PSD:** PASS
- **5 round-trips individuais:** PASS
- **Teste interativo completo no navegador:** NÃO EXECUTADO

> **Nota:** Os 54 arquivos representam *imports* PSD, e não 54 round-trips.

---

## Limitações Conhecidas

- Máscaras PSD independentes não são totalmente preservadas.
- Pixels fora da área da tela podem ser recortados.
- **Prioridade alta pendente:** memória plena por camada (tela inteira), blend/grupo de camadas (pass-through), canais/metadata/ICC do PSD, modos de mesclagem desconhecidos.

---

## Status PSD

- Inventário contém **54 arquivos** com tamanho total de **1.056.437.472 bytes (~0,984 GiB)**.
- Os três ZIPs PSD separados não estão presentes no repositório.
- **39 painéis de referência visual** ão são máscaras anotadas.
- Nenhuma execução de fine-tuning/treinamento foi realizada.

---

## Créditos

Projeto @edymbk. Documentação e assistência por **E.D.I.T.H.**

**Reuso:** Solicita-se reter a atribuição "MangaCut Studio" e apontar para o repositório original
https://github.com/samueloliveira2fg-collab/MangaCut-Studio-V12.4.
As obrigações legais dependem da licença aplicável; preservem avisos de licença de terceiros e não implicem auditoria de licença.
