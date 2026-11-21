# Limitações e Pendências — MangaCut Studio V12.4

## Limitações Conhecidas

### Escrita PSD
- O escritor PSD não preserva totalmente máscaras independentes;
- Pixels fora da área do canvas podem ser cortados.

## Pendências de Alta Prioridade

- Tratamento de memória por camada (canvas completo por camada);
- Mistura de grupos e modo "pass-through";
- Canais PSD, metadados e perfis ICC;
- Modos de mesclagem desconhecidos.

## Resumo dos Testes

### Confirmados

- Sintaxe de cinco scripts: **PASS**;
- Geometria das ferramentas de transformação: **PASS**;
- Fixture PSD sintético (1501 camadas e 2 grupos): **PASS**;
- Fixture Grayscale: **PASS**;
- 54 imports PSD: **PASS**;
- Cinco rodadas individuais (round-trips): **PASS** (não 54).

### Não Executados

- Teste interativo completo do navegador: **NOT RUN**.

## Observações

Os resultados confirmados estão claramente separados do trabalho pendente. Nenhuma outra referência de versão ou lançamento além do V12.4.

---

Créditos: @edymbk e E.D.I.T.H. (assistência de documentação por IA).
Notices de terceiros preservados.
