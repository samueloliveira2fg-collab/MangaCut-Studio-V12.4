# MangaCut Studio — status real da IA e treinamento

## Estado comprovado da V12.4

- Integração local existente: **SkyTNT Anime Segmentation / ISNet** via ONNX Runtime.
- Serviço FastAPI local: `http://127.0.0.1:8765`; endpoints `/health` e `/segment`.
- O serviço só escuta em `127.0.0.1`.
- Modelo base baixado sob demanda do Hugging Face: `skytnt/anime-seg`, arquivo `isnetis.onnx`, revisão `a0a563c41338cbe0d23dfb4bfc3e243c518e5768`, SHA-256 esperado `f15622d853e8260172812b657053460e20806f04b9e05147d49af7bed31a6e99` (~176 MB).
- Input backend: até 2,5 MP e entrada de rede 1024×1024; o frontend reduz a imagem de inferência. A máscara retornada é ampliada para a dimensão do documento e colocada em uma camada de máscara/resultado, mantendo as camadas-fonte.
- ONNX Runtime CPU é o caminho padrão; DirectML/CUDA dependem da instalação/runtime/driver compatível.
- A mesma rede base é usada para colorido e P&B. O seletor de estilo no UI é metadado até existirem pesos customizados por estilo.

## O que NÃO foi feito / não existe no pacote V12.4

- **Nenhuma execução de treinamento/fine-tuning foi realizada.**
- Nenhum PSD foi confirmado como usado em inferência de IA ou como amostra de treinamento.
- Os 54 PSDs da biblioteca foram utilizados nos testes do motor PSD (importação e alguns round-trips), não em treinamento da IA.
- Os 39 painéis da pasta `exemplos/` são referências visuais e fixtures da interface; não são máscaras anotadas nem dataset supervisionado.
- Não há `ai_training/samples/`, `ai_training/dataset/`, `dataset_manifest.csv`, modelos customizados `mangacut_isnet_v12_*.onnx`, checkpoints `.ckpt`/`.pth` ou pesos treinados incluídos nesta entrega.
- Os testes em `ai_backend/test_ai_service.py` usam uma `FakeSession` determinística. São testes de API/preprocessamento e não comprovam inferência real do modelo ONNX.
- A UI da IA é atualmente uma seção/painel expansível na interface, não uma workspace/aba exclusiva completa.

## Código de preparação de dados que já existe

Arquivos:
- `ai_training/prepare_dataset.py`
- `ai_training/run_finetune.py`
- `ai_training/requirements-training.txt`
- `ai_training/preparar_dados_windows.bat`
- `ai_training/treinar_ia_windows.bat`

O preparador exige amostras revisadas pelo usuário e arquivos pares na mesma pasta:
1. imagem de entrada PNG/JPG;
2. máscara PNG em tons de cinza, mesma dimensão;
3. `*.mcut-sample.json` com `format: "mangacut-supervised-sample"`, `reviewed_by_user: true`, nomes dos arquivos e estilo.

O sistema procura manifests recursivamente. O manifesto só pode referenciar arquivos-irmãos; exige dimensão mínima de 32×32. O preparador exige pelo menos 5 pares válidos para formar um dataset. O fine-tuning exige pelo menos 10 pares por seleção de estilo. O próprio código recomenda **50–100+ exemplos diversos por estilo** para uma avaliação inicial, não como garantia de qualidade.

O script de treinamento:
- baixa o repositório SkyTNT e o checkpoint oficial;
- verifica SHA-256 do checkpoint;
- usa split treino/validação (default 0,8), batch default 1 e 12 épocas default;
- exporta ONNX para `ai_backend/models/mangacut_isnet_v12_bw.onnx`, `_color.onnx` ou `_mixed.onnx`.

**Atenção de qualidade:** o loader upstream documentado no código binariza máscaras alvo acima de 0,3 e corta 10 px das bordas. Máscaras cinza suaves não são necessariamente aprendidas como alpha suave sem modificar e validar esse pipeline.

## Direção recomendada para a fase futura (após PSD/camadas)

- Não treinar com PSD bruto sem rótulos. PSD não é ground-truth de máscara de personagem.
- Criar pares imagem + máscara revisada, mantendo PNG original, máscara e manifesto; separar treino/validação por obra/arquivo para evitar leakage entre painéis quase iguais.
- Criar conjuntos distintos e equilibrados: mangá P&B (retículas, linhas finas, balões), HQ colorida, arte anime colorida, cabelo/roupa branca, personagens parcialmente fora da borda, fundos de alto contraste e linhas fechadas.
- Guardar exemplos difíceis e métricas: IoU/Dice, boundary F-score, false removal em áreas brancas internas e false keep em fundo; medir em resolução integral após upsample.
- Criar workspace própria para IA, revisão manual e brush de apagar/restaurar; versionar dataset/checkpoints e registrar hashes e splits.
- Não alegar 90% de certeza global sem benchmark específico e protocolo definido. Exibir confiança calibrada ou indicador de incerteza apenas se validado.

## Links oficiais
- SkyTNT code: https://github.com/SkyTNT/anime-segmentation
- SkyTNT model: https://huggingface.co/skytnt/anime-seg
- ONNX Runtime: https://github.com/microsoft/onnxruntime
