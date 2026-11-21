# Registro da Versão — MangaCut Studio V12.4

---

## Versão V12.4 — Transform Tools Fix

---

### Corrigido: Coordenadas de ponteiro em ferramentas de transformação

As coordenadas dos ponteiros foram convertidas do espaço de tela para o espaço local da camada, utilizando a **transformação inversa** para:

- Translação
- Escalonamento
- Rotação
- Espelhamento

#### Mapeamento por Ferramenta

- **Object Selection:** mapeia o retângulo visível em um quadrilátero no espaço de coordenadas da camada.
- **Pincel (Brush):** segue as transformações da camada.
- **Borracha (Eraser):** segue as transformações da camada.
- **Restaurar (Restore):** segue as transformações da camada.
- **Varinha (Wand):** segue as transformações da camada.
- **Contador de cores (Eyedropper):** segue as transformações da camada.
- **Seleção rápida (Quick Selection):** segue as transformações da camada.
- **Pré-visualização de máscara (Mask Preview):** segue as transformações da camada.
- **Contorno de seleção (Selection Outline):** segue as transformações da camada.

> **Nota:** Estas são mudanças documentadas da versão V12.4 e não testes executados nesta revisão.

---

### Resumo de Testes

| Teste | Status |
|-------|--------|
| **5 scripts — sintaxe** | PASS |
| **Transform geometry** | PASS |
| **PSD synthetic fixture (1501 camadas / 2 grupos)** | PASS |
| **Grayscale fixture** | PASS |
| **54 imports PSD** | PASS |
| **5 round-trips individuais** | PASS |
| **Teste interativo completo no navegador** | NÃO EXECUTADO |

> **Nota:** Os 54 arquivos representam *imports* PSD, não 54 round-trips. Os 5 round-trips individuais são distintos.

---

### Limitações PSD Conhecidas

- Máscaras PSD independentes não são totalmente preservadas.
- Pixels fora da área da tela podem ser recortados.
- **Prioridade alta pendente:** memória plena por camada (tela inteira), blend/grupo de camadas (pass-through), canais/metadata/ICC do PSD, modos de mesclagem desconhecidos.

---

### Status PSD

- Inventário: **54 arquivos**, total **1.056.437.472 bytes (~0,984 GiB)**.
- Três ZIPs PSD separados não estão presentes no repositório.
- **39 painéis de referência visual** não são máscaras anotadas.
- Nenhuma execução de fine-tuning/treinamento foi realizada.

---

### Créditos

Projeto @edymbk. Documentação e assistência por **E.D.I.T.H.**
