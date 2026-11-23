# Classificação de AVC em TC Cerebral — SIN 393

Projeto acadêmico de visão computacional para classificar imagens de tomografia computadorizada cerebral em três classes: **normal**, **isquemia** e **hemorragia**. O experimento compara arquiteturas e investiga o efeito de aumento de dados (*data augmentation*) com PyTorch e modelos do `torchvision`.

> **Uso acadêmico:** este projeto não é um dispositivo médico e não deve ser usado para diagnóstico ou decisão clínica.

## Acesso ao projeto

- **Notebook final executado no Google Colab:** [abrir notebook](https://colab.research.google.com/drive/1MlmlqNdRhDE403TT9m_Il0BspzX6sLsz)
- **Notebook de referência versionado neste repositório:** [brain_stroke_ct_sin393.ipynb](./brain_stroke_ct_sin393.ipynb)
- **Dataset:** [Brain Stroke CT Dataset — Kaggle](https://www.kaggle.com/datasets/ozguraslank/brain-stroke-ct-dataset)
- **Vídeo de apresentação:** [assistir no YouTube](https://youtu.be/P9x4yA63nDY)

O notebook final no Colab é a referência para a execução do experimento. O arquivo `.ipynb` deste repositório é uma cópia inicial do fluxo experimental; consulte o notebook do Colab para a versão executada e seus registros mais recentes.

## Pergunta experimental

Como a escolha da arquitetura e o uso de aumento de dados afetam a classificação das três classes de AVC em imagens de TC? O experimento avaliou quatro condições, mantendo a mesma divisão dos dados:

| Arquitetura | Aumento de dados |
|---|---|
| ResNet-18 pré-treinada | Não |
| ResNet-18 pré-treinada | Sim |
| MobileNetV3-Large pré-treinada | Não |
| MobileNetV3-Large pré-treinada | Sim |

As quatro condições representam duas arquiteturas avaliadas com e sem *augmentation*; não são quatro arquiteturas distintas.

## Protocolo experimental

- **Framework:** PyTorch e `torchvision`.
- **Ambiente de treino:** runtime remoto do Google Colab; a execução não depende da CPU ou GPU local. Uma GPU Colab pode ser selecionada quando estiver disponível na conta.
- **Reprodutibilidade:** semente fixa `393`.
- **Partições:** treino, validação e teste em hold-out estratificado (70% / 15% / 15%).
- **Seleção de modelo:** macro-F1 na validação para selecionar o melhor checkpoint; o conjunto de teste fica reservado à avaliação final.
- **Aumento de dados:** pequenas rotações e translações, além de variações moderadas de brilho e contraste, aplicadas apenas ao treino. Não são usados flips, para evitar alterar a orientação anatômica da imagem.
- **Desbalanceamento:** pesos de classe são calculados a partir do conjunto de treino.
- **Métricas:** matriz de confusão e acurácia, precisão, recall e F1-score. Para a avaliação multiclasse, são reportadas médias macro (peso igual por classe) e ponderada (pelo suporte), além dos resultados por classe.
- **Análise qualitativa:** o projeto apresenta exemplos de acertos e erros e discute hipóteses para as falhas, sem tratar a confiança do modelo como probabilidade clínica calibrada.

### Resultado principal

Na avaliação registrada para a **ResNet-18 com aumento de dados**, a acurácia foi **96,19%** e o F1-score macro foi **94,90%**. O recall da classe isquemia foi **86,47%**, indicando que essa classe ainda concentra erros relevantes. Esses valores são resultados deste conjunto e deste protocolo; não demonstram desempenho clínico nem validação externa.

## Como executar

1. Abra o [notebook final no Google Colab](https://colab.research.google.com/drive/1MlmlqNdRhDE403TT9m_Il0BspzX6sLsz) e faça uma cópia para sua conta, se necessário.
2. No menu **Ambiente de execução → Alterar tipo de ambiente de execução**, selecione uma GPU oferecida pelo Colab, se disponível. O tipo de acelerador depende da disponibilidade e da conta. O notebook também pode executar em CPU do runtime remoto, com maior tempo de processamento.
3. Disponibilize o dataset do Kaggle conforme a célula de preparação dos dados do notebook. Se a conta exigir autenticação, configure `KAGGLE_API_TOKEN` em **Secrets** do Colab e permita o acesso pelo notebook. Nunca cole ou versione tokens.
4. Execute as células em ordem. Revise a auditoria de imagens, rótulos, arquivos de metadados e possíveis identificadores de paciente/estudo antes de treinar.
5. Se houver identificadores de paciente ou estudo, use uma divisão agrupada antes do treinamento para evitar que imagens do mesmo grupo apareçam em partições distintas. Não confirme ausência desses identificadores sem verificar os metadados.
6. Execute o treinamento das quatro condições e, após congelar o protocolo, faça a avaliação final no teste. Consulte os resultados, matrizes de confusão, exemplos qualitativos e registros gerados pelo notebook.

O notebook instala as dependências Python necessárias no runtime, incluindo PyTorch/`torchvision`, KaggleHub, scikit-learn, pandas, Pillow e tqdm. A sessão de Colab precisa de acesso ao dataset e pode ser encerrada pelo serviço; salve os artefatos de interesse no Google Drive ao final.

## Reprodutibilidade e limitações

- Registre a versão/cópia do dataset, os termos de uso aplicáveis, as contagens observadas, o acelerador utilizado e as versões das bibliotecas junto com cada execução.
- A divisão por imagem pode superestimar o desempenho se existirem imagens repetidas ou cortes relacionados entre treino, validação e teste. A separação por paciente/estudo é preferível quando esses metadados estiverem disponíveis.
- Os resultados refletem uma divisão e uma semente; não substituem repetições com várias sementes, intervalos de confiança ou validação externa.
- Imagens, checkpoints, credenciais e dados clínicos privados não devem ser publicados neste repositório.

## Integrantes

- Lucas Tomaz Carmo Silva
- Gabriel Arcanjo dos Santos
- Lucas Gabriel Ferreira Gonçalves

Universidade Federal de Viçosa — Campus Rio Paranaíba · SIN 393 · 2026
