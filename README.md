Link do pdf Atividade 1 - Tutorial:
https://drive.google.com/file/d/1ryuaMkd1lus8KQWu6_XwuM0WZORUTmAE/view?usp=sharing

# Análise de Sentimentos em Pull Requests do Repositório Goose

Este projeto aplica técnicas de Processamento de Linguagem Natural (PLN) e Modelos de Linguagem (LLMs) para realizar uma análise de sentimentos nos pull requests do repositório de código aberto [Goose](https://github.com/goose). O objetivo é compreender as dinâmicas de comunicação e o panorama emocional das interações entre os desenvolvedores neste projeto.

O notebook desenvolvido extrai, processa, analisa e visualiza os sentimentos expressos nos comentários de pull requests, fornecendo insights sobre o clima colaborativo da comunidade.

## 🔗 Links Importantes

* **Repositório deste Projeto:** [https://github.com/inathanms/Evolucao_Software_2025-2_goose](https://github.com/inathanms/Evolucao_Software_2025-2_goose)
* **Vídeo Explicativo (Tutorial):** [https://drive.google.com/file/d/1BBejlLXhqRkppvpKW08VY4GcJHsnLaVe/view?usp=sharing](https://drive.google.com/file/d/1BBejlLXhqRkppvpKW08VY4GcJHsnLaVe/view?usp=sharing)
* **Repositório Analisado (Goose):** [https://github.com/block/goose](https://github.com/block/goose)

## 💻 Tecnologias e Bibliotecas

O projeto foi desenvolvido inteiramente em **Google Colab** para facilitar o acesso a recursos computacionais (GPU), colaboração e reprodutibilidade.

As principais bibliotecas Python utilizadas foram:

* **`requests`**: Para realizar requisições HTTP e interagir com a API do GitHub, coletando pull requests e comentários.
* **`google.colab.userdata`**: Para acessar de forma segura o token de acesso da API do GitHub (segredos).
* **`re (Regular Expressions)`**: Para limpar e normalizar os textos dos comentários, substituindo abreviações por suas formas completas.
* **`transformers (Hugging Face)`**: Biblioteca central para a análise de sentimentos, permitindo o uso de modelos de PLN pré-treinados.
* **`pandas`**: Para organizar os dados (comentários, sentimentos, pontuações) em DataFrames, facilitando a manipulação e análise.
* **`matplotlib.pyplot`** e **`seaborn`**: Para a criação de gráficos e visualizações estatísticas, como histogramas e distribuições de sentimentos.

## 🚀 Como Executar

Para reproduzir esta análise, siga os passos abaixo no ambiente do Google Colab:

1.  **Carregar o Notebook:** Faça o upload do arquivo `.ipynb` para o seu Google Drive e abra-o com o Google Colab.
2.  **Inserir o Token do GitHub:** É necessário um *Personal Access Token (PAT)* do GitHub. Insira este token na seção "Secrets" (variáveis de usuário) do Google Colab com o nome `GITHUB_ACCESS_TOKEN`. Isso é essencial para a autenticação segura e para evitar limites de requisição da API.
3.  **Executar as Células:** Execute as células do notebook em ordem sequencial. Cada célula está documentada, e a ordem é importante, pois etapas posteriores dependem dos dados carregados e processados nas etapas anteriores.
4.  **Interpretar os Resultados:** Ao final da execução, o notebook exibirá gráficos e tabelas com a distribuição dos sentimentos, permitindo a análise das tendências de comunicação no repositório.

## ⚙️ Metodologia e Fluxo de Execução

O notebook segue um fluxo estruturado em cinco etapas principais para garantir a reprodutibilidade e a clareza do processo.

### Parte 1: Coleta de Dados do GitHub

O código interage com a API do GitHub para coletar dados do repositório `block/goose`. A biblioteca `requests` é usada para buscar Pull Requests fechados e todos os seus comentários associados, autenticando com o `GITHUB_ACCESS_TOKEN`.

> **Ponto-chave:** Esta fase assegura a obtenção dos dados brutos diretamente da fonte, garantindo autenticidade e integridade das informações.

### Parte 2: Pré-processamento e Normalização

Os comentários coletados passam por uma limpeza textual rigorosa:
* Remoção de comentários de bots e mensagens automáticas.
* Expansão de abreviações comuns de desenvolvimento (ex: `WIP`, `LGTM`, `PR`, `IMO`) usando `re` e um mapa customizado.
* Truncamento dos comentários para 512 caracteres, garantindo compatibilidade com os modelos de PLN.

> **Ponto-chave:** Os dados são limpos e estruturados para serem interpretados corretamente pelos modelos de linguagem.

### Parte 3: Análise de Sentimento com Modelos Transformers

Esta é a fase central da análise, onde a biblioteca `transformers` da Hugging Face é aplicada. Para aumentar a confiabilidade, três modelos distintos foram utilizados:

1.  `cardiffnlp/twitter-roberta-base-sentiment-latest`
2.  `lxyuan/distilbert-base-multilingual-cased-sentiments-student`
3.  `citizenlab/twitter-xlm-roberta-base-sentiment-finetunned`

Cada modelo classifica os comentários pré-processados, retornando um **rótulo** (positivo, negativo ou neutro) e uma **pontuação de confiança**.

> **Ponto-chave:** Aplicação prática de múltiplos modelos de PLN para extração automatizada e robusta de sentimentos em textos técnicos.

### Parte 4: Análise e Visualização dos Resultados por Modelo

Os resultados de cada modelo são organizados em DataFrames `pandas`. As bibliotecas `matplotlib` e `seaborn` são usadas para gerar visualizações detalhadas, incluindo:

* Distribuição de rótulos de sentimento.
* Distribuição das pontuações de confiança.
* Médias das pontuações por categoria de sentimento.

> **Ponto-chave:** Esta etapa transforma os resultados brutos da classificação em representações gráficas claras e interpretáveis.

### Parte 5: Análise Consolidada e Geração de Insights

Por fim, os resultados dos três modelos são combinados em um DataFrame unificado (`combined_df`) para uma análise consolidada. Isso permite comparar o comportamento dos modelos e identificar padrões de comunicação no repositório.

Gráficos finais destacam:
* A distribuição geral de sentimentos (considerando todos os modelos).
* A **Pontuação Média Global de Sentimento**, que sintetiza a tendência geral das interações analisadas.

> **Ponto-chave:** Extração de insights sobre padrões de comunicação, fornecendo uma visão abrangente do comportamento colaborativo no repositório Goose.
