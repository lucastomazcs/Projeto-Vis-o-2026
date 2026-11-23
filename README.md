# Brain Stroke CT — SIN393

Experimento reprodutível de classificação de imagens de CT cerebral, conforme o plano do projeto SIN393.

## Estado inicial

- Notebook inicial para Google Colab: `brain_stroke_ct_sin393.ipynb`
- Dataset: [Brain Stroke CT Dataset no Kaggle](https://www.kaggle.com/datasets/ozguraslank/brain-stroke-ct-dataset)
- Execução prevista no runtime do Colab (CPU/GPU da nuvem); este projeto não treina usando o hardware local.
- O notebook começa pela auditoria do conteúdo baixado. Contagens, classes, formatos, licença e metadados ainda precisam ser confirmados na cópia efetivamente obtida.

## Experimentos planejados

Comparar ResNet-18 e MobileNetV3-Large, ambas pré-treinadas, com e sem augmentation clinicamente moderado. A divisão será estratificada em treino/validação/teste (70/15/15), semente 393; se identificadores de paciente/estudo existirem, será necessário usar divisão agrupada antes de treinar. Macro-F1 na validação selecionará checkpoints. O teste será usado uma única vez após congelar a configuração.

## Como começar

1. Abra `brain_stroke_ct_sin393.ipynb` no Google Colab.
2. Se disponível, escolha Runtime > Change runtime type > T4 GPU. O tipo de acelerador depende da disponibilidade e da conta Colab.
3. Execute a célula de download com KaggleHub. Se o Kaggle exigir autenticação, salve um token `KAGGLE_API_TOKEN` em Secrets do Colab; não cole nem versione o token.
4. Execute as células de auditoria e revise as classes e os metadados antes de iniciar qualquer treino.

O token Kaggle deve permanecer nos Secrets/runtime do Colab; não o grave neste repositório. Os arquivos de imagem e checkpoints também não devem ser versionados.

## Limites

Trabalho acadêmico de classificação de imagens; não se destina a diagnóstico ou decisão clínica. Sem metadados de paciente, duplicatas parecidas ou estudos relacionados, a separação por imagem pode ter vazamento e isso deve constar nas limitações. Não faça upload de imagens clínicas privadas.

## Link Apresentação
https://youtu.be/P9x4yA63nDY
