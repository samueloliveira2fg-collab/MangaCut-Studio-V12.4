# Guia para Continuação — MangaCut Studio V12.4

## Checklist de Entrega Segura

1. Preservar o ZIP original e os originais PSD;
2. Inspecionar o handoff completo (`MangaCut_Codex_Handoff_Completo.md`) e o status da IA (`AI_STATUS_E_TREINAMENTO.md`);
3. Não afirmar compatibilidade total com PSD;
4. Reproduzir os testes e marcar PASS, FAIL, BLOCKED ou NOT RUN;
5. Os 54 imports PSD não são 54 rodadas completas (round-trips); apenas cinco rodadas individuais PASS;
6. Obter as três partes faltantes do ZIP PSD antes de tentar reproduzir o corpus completo PSD;
7. Não realizar fine-tuning até que um dataset revisado de imagens/máscaras em pares exista;
8. Os 39 painéis de referência não são máscaras anotadas;
9. Preservar arquivos de licença e notices de terceiros, além da atribuição do projeto;
10. Não sobrescrever os originais;
11. Documentar o ambiente e os hashes (ver `CHECKSUMS_SHA256.txt`).

## Observações

Este guia aplica-se estritamente ao V12.4. Nenhuma outra versão ou referência de lançamento.
