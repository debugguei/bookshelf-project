[← Back to language selection](./README.md)

# Booksheelf Social Network

### About the Project
An event-driven social network for book readers. Users can identify and add books to their digital shelves simply by taking a picture of the book cover. The system processes the image using Computer Vision and Large Language Models (LLMs) to automatically extract structured data (Title, Author, Publisher).

### Architecture & Technologies
This project relies on a distributed architecture built on the AWS ecosystem, running natively on Windows without Docker:
* **Frontend:** Ionic / Angular (Mobile App)
* **Storage & Queues:** AWS S3 (image storage) and AWS SQS (message queuing)
* **Computer Vision & AI:** AWS Rekognition (OCR) and Llama 3 via Amazon Bedrock (LLM)
* **Database:** Amazon DynamoDB
* **Distributed Worker:** Multithreaded C++ application compiled with MinGW for queue polling and parallel processing

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
│   └── .env                        # AWS credentials (Git-ignored)
│
└── repo-comp-distribuida/          # Distributed Worker Repository (C++)
    ├── src/mensageria/             # AWS SQS polling scripts
    ├── src/paralelismo/            # Thread pool and concurrency manager
    ├── src/orquestrador/           # Service orchestration (Image -> LLM -> DynamoDB)
    ├── .env                        # Environment variables
    └── Makefile                    # MinGW compilation rules for Windows