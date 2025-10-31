# **DIO - Microsoft Certification Challenge #4 - DP 100**
## Lab Project 03: Guia Passo a Passo - Chatbot RAG com Azure AI Foundry 🔍📚🤖💬

Este repositório documenta o projeto "Criando um Chatbot Baseado em Conteúdo de PDFs", desenvolvido utilizando a plataforma **Azure AI Foundry** (anteriormente conhecida como Azure AI Studio) como parte do "Microsoft Certification Challenge #4 - DP 100" da [DIO (Digital Innovation One)](https://www.dio.me/en).

O objetivo foi criar um assistente de IA para responder perguntas sobre um TCC com base na literatura (PDFs), usando uma abordagem *low-code* RAG (Retrieval-Augmented Generation).

---

### 📖 Visão Geral do Desafio

O projeto consiste no desenvolvimento de um chat interativo capaz de responder perguntas com base no conteúdo de arquivos PDF fornecidos pelo usuário. Para isso, foram aplicados conceitos de IA Generativa, *embeddings* (vetorização de texto) e buscas vetorizadas, estruturando um sistema RAG (Retrieval-Augmented Generation).

O resultado é um modelo de assistência virtual personalizado, focado em um conjunto de informações proprietárias (os PDFs), sem depender unicamente do conhecimento geral de modelos pré-treinados, permitindo ao estudante "conversar" com seus documentos.

### 🖼 Cenário

O cenário simulado é o de um estudante de Engenharia de Software em fase de elaboração do Trabalho de Conclusão de Curso (TCC), cujo tema é "Análises Estatísticas Aprofundadas para a Ciência de Dados e Inteligência Artificial".

Os documentos PDF utilizados como base de conhecimento (disponíveis no diretório inputs/PDFs) incluem títulos como:
* Applied Predictive Modelling R.pdf
* Aprendizagem Maquina_Abordagem Estatística__Izbicki.pdf
* Data Science for Business.pdf
* Introduction to Machine Learning with Python ( PDFDrive ).pdf
* E outros materiais de referência sobre ML e Estatística.

O chatbot atua como um assistente de pesquisa, permitindo ao estudante extrair informações relevantes e conectar ideias entre as diferentes literaturas.

### 🎯 Objetivo

O objetivo deste projeto é implementar um sistema completo que permite:

1.  Carregar arquivos PDF contendo a base de conhecimento relevante para o TCC.
2.  Implementar um sistema de busca vetorial para indexar e recuperar informações dos PDFs.
3.  Utilizar Inteligência Artificial (IA Generativa) para gerar respostas baseadas *exclusivamente* no conteúdo dos documentos PDFs carregados.
4.  Desenvolver um chat interativo onde o usuário (estudante) possa realizar perguntas e obter respostas contextuais e fundamentadas nos arquivos.

### 🛠️ Tecnologias Utilizadas (Azure AI Foundry)

Esta solução foi construída **sem código personalizado**, utilizando exclusivamente os serviços pré-configurados da plataforma Azure AI:

* **Plataforma:** Azure AI Foundry (Hub e Projeto de IA)
* **Ferramenta:** Azure AI Chat Playground (dentro do Foundry)
* **Ingestão de Dados:** Funcionalidade "Adicionar seus dados (visualização)"
* **Indexação e Busca:** Azure AI Search (criado e configurado automaticamente)
* **Modelo de Geração (LLM):** `gpt-4o`
* **Modelo de Embedding:** `text-embedding-3-large`
* **Prompt Engineering:** Campo "Mensagem do sistema" (System message)
* **Implantação (Deploy):** "Aplicativo Web" (Azure App Service)

---

### 🌠🪄 Guia de Reprodução: Passo a Passo no Azure AI Foundry

Qualquer pessoa pode reproduzir este projeto seguindo exatamente estes passos:

#### 🛠️ 1. Configuração Inicial: Hub e Projeto de IA

1.  **Acesse o Portal Azure:** Faça login em [portal.azure.com](https://portal.azure.com).
2.  **Acesse o AI Foundry:** Na barra de busca, procure por **"Azure AI Foundry"** e acesse o serviço. (Se não encontrar, procure por "Azure AI" e selecione o Hub principal).
3.  **Crie um Hub de IA (AI Hub):** Um Hub (ou "Recurso de IA do Azure") é o contêiner de nível superior. Se você não tiver um, crie um novo.
4.  **Crie um Projeto de IA (AI Project):** Dentro do seu Hub de IA, crie um novo "Projeto". Dê um nome a ele (ex: `DIO-DP100-Chatbot-TCC`). Este projeto conterá seus modelos, dados e playgrounds.

#### 🔧 2. Preparando os Modelos (Implantações)

Antes de ir ao playground, é preciso garantir que os modelos `gpt-4o` e `text-embedding-3-large` estejam disponíveis (implantados) no projeto.

1.  No menu esquerdo do seu Projeto de IA (dentro do portal Azure AI Foundry), vá para **"Catálogo de Modelos" (Model catalog)**.
2.  **Implante o GPT-4o:**
    * Encontre o modelo `gpt-4o`.
    * Clique em "Implantar" (Deploy).
    * Selecione a opção "Pagamento conforme o uso" (Pay-as-you-go).
    * Dê um nome à implantação (ex: `gpt-4o-deploy`).
3.  **Implante o Embedding:**
    * No Catálogo de Modelos, encontre `text-embedding-3-large`.
    * Clique em "Implantar".
    * Dê um nome à implantação (ex: `text-embedding-3-deploy`).

#### 🔧 3. Configurando o Chat Playground (O Cérebro do RAG)

Este é o passo central, onde os dados e o modelo são conectados.

1.  No menu esquerdo do seu Projeto de IA, vá para **"Playgrounds"** e selecione a opção **"Try the Chat playground"**.
2.  **Selecione o Modelo de Chat:** Na seção "Configuração" (Configuration) à direita, no dropdown "Implantação" (Deployment), selecione a implantação do `gpt-4o` que você criou (ex: `gpt-4o-deploy`).

#### 🔍📚 4. Adicionando os PDFs (A Base de Conhecimento)

1.  Ainda na tela do Chat Playground, abaixo da configuração do modelo, clique na aba **"Adicionar seus dados (pré visualização)"** ou **"Add your data (preview)"**.
2.  Clique em **"+ Adicionar dados"**.
3.  **Fonte de Dados:** No assistente, selecione **"Carregar arquivos" (Upload files)**.
4.  **Carregar os PDFs:** Arraste ou selecione todos os PDFs do TCC (os 8+ arquivos disponíveis no diretório inputs/PDFs).
5.  **Recurso do AI Search:** O Azure *precisa* de um **Azure AI Search** para indexar os PDFs. O assistente solicitará que a escolha de um:
    * Crie um novo recurso do AI Search (plano Gratuito ou Básico). Dê um nome a ele (ex: `ai-search-tcc-dp100`).
    * Marque a caixa de confirmação de custos.
6.  **Recurso de Embedding:** O assistente perguntará qual modelo de embedding usar para vetorizar seus PDFs.
    * Selecione a implantação do `text-embedding-3-large` que criou anteriormente (ex: `text-embedding-3-deploy`).
7.  **Nome do Índice:** Dê um nome ao seu índice de busca (ex: `indice-tcc-pdfs`).
8.  **Concluir:** Clique em "Avançar" e "Salvar e Concluir". O Azure começará a "ingerir" os dados. Isso pode levar alguns minutos. Será possível observar que os arquivos estão sendo processados e indexados.

#### 🔧 5. Definindo o "System Prompt" (Instruções do Modelo)

Agora que o chatbot pode "ler" os PDFs adicionados, é possível dizer a ele *como* se comportar.

1.  Na tela do Chat Playground, na caixa de texto principal chamada **"Mensagem do sistema" (System message)**, cole as seguintes instruções no campo "Give the model instructions and context":

```text
Você é um assistente de pesquisa acadêmica, especialista em Estatística e Machine Learning.
Seu propósito é ajudar um estudante de TCC a encontrar informações nos seus documentos.

REGRAS IMPORTANTES:
1. Responda as perguntas *estritamente* e *apenas* com base no conteúdo dos arquivos PDF fornecidos (a fonte de dados).
2. Seja preciso, técnico e objetivo, como um especialista.
3. Se a informação não estiver nos documentos, informe claramente: "Não encontrei essa informação nos documentos PDFs fornecidos para embasar o TCC."
4. Não use nenhum conhecimento externo ou geral que você possua. Foque 100% nos dados carregados.
5. Quando responder, cite o nome do arquivo PDF de onde a informação foi extraída.
```

#### 🤖💬💯 6. Testando o Chatbot

No playground, use a caixa de chat para testar. Use as perguntas do arquivo `inputs/sentencas.txt`.

**Exemplos de Teste:**
* *"Qual a definição de 'overfitting' segundo o livro 'Introduction to Machine Learning with Python'?"*
* *"Como o livro de Izbicki ('Aprendizagem de Maquina: Abordagem Estatística') explica o Teorema de Bayes?"*
* *"Qual a diferença entre regularização L1 e L2 segundo os PDFs?"*

Você verá que o chatbot responde e inclui uma **[citação]** clicável, mostrando qual *chunk* de qual PDF foi usado para gerar a resposta.

#### 🖥️ 7. Implantando como um Aplicativo Web

Para que qualquer pessoa possa usar seu chatbot sem acessar seu Azure AI Foundry, é possível publicá-lo.

1.  Na parte superior do Chat Playground, clique no botão **"Implantar" (Deploy)**.
2.  Selecione **"Um novo aplicativo Web..." (A new web app...)**.
3.  **Configuração:**
    * Dê um nome ao seu aplicativo (ex: `chatbot-tcc-dp100-demo`).
    * Selecione sua Assinatura.
    * Crie um novo "Plano de Serviço" (App Service Plan) – o plano Gratuito (F1) funciona para este demo.
4.  **Implantar:** Clique em "Implantar". O Azure provisionará um Azure App Service e publicará uma interface de chat pronta para uso.
5.  **Acessar:** Após a conclusão, um link aparecerá. Clique nele para ver seu chatbot funcionando em um site público!

---

### 🔍📚🤖💬 Resultados (Prints da Aplicação)

*(Nesta seção, adicione seus próprios prints para documentar o processo)*

**[Inserir Print 1: A tela do "Adicionar seus dados" no Azure AI Foundry com os PDFs carregados e o Azure AI Search configurado.]**

**[Inserir Print 2: A tela do Playground com o "System message" preenchido e o modelo `gpt-4o` selecionado.]**

**[Inserir Print 3: O chat no playground respondendo a uma pergunta (ex: sobre "overfitting") e mostrando a [citação] do PDF.]**

**[Inserir Print 4: O aplicativo web final (Azure App Service) publicado e em funcionamento no navegador.]**

---

### 💡 Insights e Conclusões

Este projeto demonstrou o poder do **Azure AI Foundry** para prototipagem rápida de soluções de IA Generativa.

1.  **Abstração Total (RAG as a Service):** A maior vantagem foi a abstração da complexidade. Não foi necessário escrever código Python ou gerenciar bibliotecas de orquestração. O "Add your data" orquestrou o `text-embedding-3-large` para *chunking* e vetorização, e o Azure AI Search para indexação e recuperação.
2.  **Zero-Code para MVP:** O botão "Deploy to Web App" é incrivelmente poderoso. Ele criou um MVP (Minimum Viable Product) funcional, hospedado e seguro em minutos, validando a solução de ponta a ponta.
3.  **Controle via Prompt:** O "System Prompt" (o campo "Give the model instructions...") provou ser a ferramenta de controle mais crítica para garantir que o `gpt-4o` não "alucinasse" e se mantivesse fiel aos dados do TCC.
4.  **Qualidade dos Modelos:** A combinação do `text-embedding-3-large` (ótimo para entender a semântica de textos técnicos) e o `gpt-4o` (excelente em raciocínio e geração) produziu respostas de alta qualidade, relevantes e precisas, baseadas na literatura fornecida (PDFs).
