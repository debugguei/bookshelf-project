# Booksheelf Social Network

Choose your language / Escolha seu idioma:
* [🇺🇸 English](#-english)
* [🇧🇷 Português](#-português)

---

### About the Project
An event-driven social network for book readers. Users can identify and add books to their digital shelves simply by taking a picture of the book cover. The system processes the image using Computer Vision and Large Language Models (LLMs) to extract structured data (Title, Author, Publisher) automatically.

### Architecture & Technologies
This project relies on a distributed architecture utilizing the AWS ecosystem natively on Windows without Docker:
* **Frontend:** Ionic / Angular (Mobile App)
* **Storage & Queues:** AWS S3 (Image storage) and AWS SQS (Message queuing)
* **Computer Vision & AI:** AWS Rekognition (OCR) and Llama3.
* **Database:** Amazon DynamoDB
* **Distributed Worker:** Multithreaded C++ application compiled via MinGW for queue polling and parallel processing.

### Repository & Folder Structure
This is a monorepo containing three independent child repositories (Git Submodules). Below is the macro structure of the ecosystem:

```text
/bookshelf-project
│
├── prjDevMob/                      # Mobile App Repository
│   ├── src/app/                    # Pages, Core services, and Shared components
│   ├── src/environments/           # API URLs and environment variables
│   ├── capacitor.config.ts         # Hardware configuration (Camera integration)
│   └── package.json                # Node dependencies
│
├── repo-processamento-imagem/      # Computer Vision & AI Repository
│   ├── src/pre_processamento/      # Image enhancement before OCR
│   ├── src/ocr/                    # AWS Rekognition integration
│   ├── src/ia_parser/              # Amazon Bedrock (LLM) JSON structuring
│   ├── utils/                      # Execution time and accuracy metrics
│   └── .env                        # AWS Keys (Ignored by Git)
│
└── repo-comp-distribuida/          # Distributed Worker Repository (C++)
    ├── src/mensageria/             # AWS SQS polling scripts
    ├── src/paralelismo/            # Thread pool and concurrent execution manager
    ├── src/orquestrador/           # Service orchestration (Image -> LLM -> DynamoDB)
    ├── .env                        # Environment variables
    └── Makefile                    # MinGW compilation rules for Windows

---

### Sobre o Projeto
Uma rede social orientada a eventos para leitores. Os usuários podem identificar e adicionar livros às suas estantes digitais simplesmente tirando uma foto da capa. O sistema processa a imagem usando Visão Computacional e Large Language Models (LLMs) para extrair dados estruturados (Título, Autor, Editora) automaticamente.

### Arquitetura e Tecnologias
Este projeto utiliza uma arquitetura distribuída baseada no ecossistema AWS, rodando nativamente no Windows sem uso de Docker:
* **Frontend:** Ionic / Angular (App Mobile)
* **Armazenamento e Filas:** AWS S3 (Armazenamento de imagens) e AWS SQS (Mensageria)
* **Visão Computacional e IA:** AWS Rekognition (OCR) e Llama3.
* **Banco de Dados:** Amazon DynamoDB
* **Worker Distribuído:** Aplicação multithread em C++ compilada via MinGW para escuta de filas e processamento paralelo.

### Estrutura do Repositório e Pastas
Este é um monorepo que contém três repositórios filhos independentes (Git Submodules). Abaixo está a macroestrutura do ecossistema:

```text
/bookshelf-project
│
├── prjDevMob/                      # Repositório do App Mobile
│   ├── src/app/                    # Páginas, Serviços globais e Componentes
│   ├── src/environments/           # URLs da API e variáveis de ambiente
│   ├── capacitor.config.ts         # Configuração de hardware (Acesso à câmera)
│   └── package.json                # Dependências do Node
│
├── repo-processamento-imagem/      # Repositório de Visão Computacional e IA
│   ├── src/pre_processamento/      # Ajustes de imagem (contraste/filtros) antes do OCR
│   ├── src/ocr/                    # Integração com AWS Rekognition
│   ├── src/ia_parser/              # Estruturação do JSON final com Amazon Bedrock (LLM)
│   ├── utils/                      # Scripts de métricas de tempo e precisão
│   └── .env                        # Chaves da AWS (Ignorado pelo Git)
│
└── repo-comp-distribuida/          # Repositório do Worker Distribuído (C++)
    ├── src/mensageria/             # Scripts de escuta (polling) da fila no AWS SQS
    ├── src/paralelismo/            # Gerenciador de threads pool e concorrência
    ├── src/orquestrador/           # Orquestrador do fluxo (Baixa Imagem -> Aciona LLM -> Salva no BD)
    ├── .env                        # Variáveis de ambiente locais
    └── Makefile                    # Regras de compilação C++ via MinGW no Windows