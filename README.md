# 🎓 Assistente Acadêmico com Gemini & RAG

Assistente inteligente que utiliza Retrieval-Augmented Generation (RAG) para responder perguntas sobre documentos PDF acadêmicos, powered by Google Gemini e LangChain.

## 🚀 Funcionalidades

- 📄 Upload e processamento de documentos PDF
- 🔍 Busca semântica usando embeddings vetoriais
- 🤖 Respostas contextualizadas baseadas no conteúdo do documento
- 💬 Interface conversacional intuitiva
- ⚡ Respostas rápidas com Gemini 1.5 Flash

## 🛠️ Tecnologias Utilizadas

### Core
- **Python 3.x**
- **Streamlit** - Interface web
- **LangChain** - Framework para aplicações com LLMs
- **Google Gemini 1.5 Flash** - Modelo de linguagem

### RAG Pipeline
- **FAISS** - Banco de dados vetorial para busca por similaridade
- **GoogleGenerativeAIEmbeddings** - Geração de embeddings (modelo embedding-001)
- **PyPDFLoader** - Extração de texto de PDFs
- **RecursiveCharacterTextSplitter** - Divisão inteligente de documentos

### Deploy
- **Ngrok** - Túnel para acesso público
- **Google Colab** - Ambiente de desenvolvimento

## 📋 Pré-requisitos

- Conta Google (para Colab)
- API Key do Google AI Studio ([obter aqui](https://makersuite.google.com/app/apikey))
- Authtoken do Ngrok ([obter aqui](https://dashboard.ngrok.com/get-started/your-authtoken))

## ⚙️ Instalação e Configuração

### 1. Clone o repositório
```bash
git clone https://github.com/seu-usuario/assistente-academico-rag.git
cd assistente-academico-rag
```

### 2. Configuração no Google Colab

#### 2.1 Adicione suas credenciais aos Secrets
1. Clique no ícone de chave 🔑 na barra lateral do Colab
2. Adicione os seguintes secrets:
   - `GOOGLE_API_KEY`: Sua API key do Google AI
   - `NGROK_AUTHTOKEN`: Seu authtoken do Ngrok
3. Ative "Notebook access" para ambos

#### 2.2 Execute as células na ordem
```python
# Célula 1: Instalação de dependências
!pip install streamlit langchain langchain-google-genai langchain-community pypdf faiss-cpu pyngrok nest_asyncio -q

# Célula 2: Configuração da API
# (Execute para configurar as credenciais)

# Célula 3: Código da aplicação
# (Cria o arquivo app.py)

# Célula 4: Inicialização do servidor
# (Inicia Streamlit e Ngrok)
```

### 3. Acesse a aplicação
Após executar a Célula 4, você receberá um URL público do Ngrok:
```
✅ Aplicativo Streamlit rodando! Acesse em: https://xxxx-xx-xx-xxx-xx.ngrok-free.app
```

## 📖 Como Usar

1. **Upload do PDF**
   - Clique em "Carregue seu PDF aqui" na barra lateral
   - Selecione um documento PDF acadêmico

2. **Processar Documento**
   - Clique no botão "Processar PDF"
   - Aguarde o processamento (pode levar alguns minutos)

3. **Fazer Perguntas**
   - Digite sua pergunta no campo de texto
   - Clique em "Enviar Pergunta"
   - Receba respostas baseadas no conteúdo do documento

## 🧠 Como Funciona

### Arquitetura RAG
```
PDF Upload → Text Extraction → Chunking → Embeddings → FAISS Vector Store
                                                              ↓
User Question → Embedding → Similarity Search → Relevant Chunks → LLM → Answer
```

### Pipeline Detalhado

1. **Processamento do PDF**
   - Extração de texto com `PyPDFLoader`
   - Divisão em chunks de 1000 caracteres com overlap de 200

2. **Vetorização**
   - Conversão de chunks em embeddings usando `embedding-001`
   - Armazenamento no FAISS para busca eficiente

3. **Question Answering**
   - Query do usuário é convertida em embedding
   - Busca dos 5 chunks mais similares (k=5)
   - Chunks + pergunta são enviados ao Gemini
   - Resposta gerada baseada apenas no contexto fornecido

## 🔒 Segurança

- ✅ API keys gerenciadas via secrets (não expostas no código)
- ✅ Prompt engineering para evitar alucinações
- ✅ Respostas limitadas ao contexto do documento
- ✅ Validação de entrada/saída

## 📊 Configurações do Modelo

- **Modelo**: `gemini-1.5-flash-latest`
- **Temperature**: 0.2 (respostas mais determinísticas)
- **Chunk Size**: 1000 caracteres
- **Chunk Overlap**: 200 caracteres
- **Top-k retrieval**: 5 documentos

## 📝 Limitações

- Suporta apenas arquivos PDF
- Limite de contexto do modelo (depende do tamanho do documento)
- Requer conexão com internet
- Depende de cotas da API do Google


## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.


---

⭐ Se este projeto foi útil, considere dar uma estrela!
