
---

## 📄 `README.pt-BR.md` (versão em português)

```markdown
[← Voltar para a seleção de idioma](./README.md)

# Booksheelf Social Network

### Sobre o Projeto
Uma rede social orientada a eventos para leitores. Os usuários podem identificar e adicionar livros às suas estantes digitais simplesmente tirando uma foto da capa. O sistema processa a imagem usando Visão Computacional e Large Language Models (LLMs) para extrair automaticamente dados estruturados (Título, Autor, Editora).

### Arquitetura e Tecnologias
Este projeto utiliza uma arquitetura distribuída baseada no ecossistema AWS, executando nativamente no Windows sem uso de Docker:
* **Frontend:** Ionic / Angular (App Mobile)
* **Armazenamento e Filas:** AWS S3 (armazenamento de imagens) e AWS SQS (mensageria)
* **Visão Computacional e IA:** AWS Rekognition (OCR) e Llama 3 via Amazon Bedrock (LLM)
* **Banco de Dados:** Amazon DynamoDB
* **Worker Distribuído:** Aplicação multithread em C++ compilada via MinGW para escuta de filas e processamento paralelo

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
│   └── .env                        # Credenciais AWS (ignoradas pelo Git)
│
└── repo-comp-distribuida/          # Repositório do Worker Distribuído (C++)
    ├── src/mensageria/             # Scripts de escuta (polling) da fila no AWS SQS
    ├── src/paralelismo/            # Gerenciador de thread pool e concorrência
    ├── src/orquestrador/           # Orquestrador do fluxo (Baixa Imagem -> Aciona LLM -> Salva no BD)
    ├── .env                        # Variáveis de ambiente locais
    └── Makefile                    # Regras de compilação C++ via MinGW no Windows