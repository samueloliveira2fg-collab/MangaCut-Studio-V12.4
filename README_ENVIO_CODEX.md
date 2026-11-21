# Pacote MangaCut Studio para Codex

Envie o ZIP-base e as três partes do acervo PSD:

1. `MangaCut_Codex_Pacote_Base.zip` — código V12.4, relatórios, contexto, IA, 39 painéis de referência, manifestos e scripts.
2. `MangaCut_PSD_Acervo_01_de_03.zip`
3. `MangaCut_PSD_Acervo_02_de_03.zip`
4. `MangaCut_PSD_Acervo_03_de_03.zip`

## Como montar as pastas

1. Extraia `MangaCut_Codex_Pacote_Base.zip`. Ele cria a pasta `MangaCut_Codex_Entrega/`.
2. Abra essa pasta `MangaCut_Codex_Entrega/`.
3. Extraia **as três partes PSD dentro dela**, aceitando mesclar a mesma pasta `PSDs/`.
4. O resultado deve ficar assim:

```text
MangaCut_Codex_Entrega/
  CODEX_HANDOFF_COMPLETO.md
  PSD_54_INVENTARIO.csv
  PSD_54_MANIFEST_SHA256.json
  PSDs/                         # 54 arquivos PSD das 3 partes
  MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX/
  FERRAMENTAS_CODEX/
  RELATORIOS_ANTERIORES/
```

## Rodar os testes

No PowerShell, dentro da pasta `MangaCut_Codex_Entrega/`:

```powershell
.\FERRAMENTAS_CODEX\Run-PSD-Import-All.ps1
.\FERRAMENTAS_CODEX\Run-PSD-Roundtrip-Each.ps1
```

A segunda bateria abre um processo Node por PSD, pois a rodada inteira em um único processo ultrapassou o limite de execução anteriormente.

**Importante:** a última versão confirmada é V12.4. Não há V13 incluída. Os 54 PSDs foram usados nos testes do motor PSD; não foram usados no treinamento da IA. O fine-tuning não foi executado.
