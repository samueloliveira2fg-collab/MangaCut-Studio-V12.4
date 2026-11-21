# Limitações e Pendências — MangaCut Studio V12.4

## Limitações Conhecidas

- **Escritor PSD:** ão preserva totalmente máscaras independentes.
- **Pixels fora do canvas** podem ser recortados.

## Pendências — Alta Prioridade

- Tratamento de memória para canvas inteiro por camada.
- Mesclagem (blend) de grupos / modo *pass-through*.
- Canais PSD, metadados e perfil ICC.
- Modos de mesclagem desconhecidos.

## Resumo dos Testes

- Sintaxe de cinco scripts: **PASS**.
- Geometria da transformação: **PASS**.
- Fixture PSD sintético com 1501 camadas e 2 grupos: **PASS**.
- Fixture *Grayscale*: **PASS**.
- 54 imports PSD: **PASS**.
- Cinco rodadas individuais *round-trip*: **PASS** (não 54).
- Teste interativo completo no navegador: **NÃO EXECUTADO**.

## Observações

- Testes já documentados estão listados acima.
- Trabalhos pendentes estão listados na seção de "Pendências — Alta Prioridade".
- Não há outras referências de versão/projeto além do V12.4.
- Manter avisos de terceiros e licenças.

## Créditos

- Projeto: @edymbk
- Documentação e assistência de IA: E.D.I.T.H. (assistente de IA de edymbk)
- Preservar avisos de terceiros e licenças.
