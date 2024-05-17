# Introduction 
1. Overview of LangChain
   - Open-source developer framework for building LLM applications
   - Python and TypeScript packages
   - Focused on composition and modularity
   - Key value adds:
     + Modular components (and implementations of those components)
     + Use cases - commom ways to combine those componenets together
2. Components
   - Prompts
   - Models
   - Indexes
   - Chains
   - Agents
![螢幕擷取畫面 (713)](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/assets/151610467/761e2b59-8f73-4bdf-a0dc-f5c75b720e80)

![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/blob/03d792a22b260c3f9c8748fe23c66fd52c54661f/RAG.png)

# Document loading 
1. Before create applications, you have to load your data into a format that can be work with.
2. Loaders
   - Loaders deal with the specifies of accessing and converting data
     + Accessing: Websites, databases, youtube, arxiv ...
     + Data types: pdf, html, json, word, ppt...
   - Returns a list of 'Document' objects

## Document splitting
1. How to split data into chuncks?
2. Splitting documents into smaller chunks
   - Retaining meaningful relationships
3. Example splitter

```
langchain.text_splitter.CharacterTextSplitter(
   separator:str='\n\n'
   chunk_size=4000,
   chunk_overlap=200,
   length_function=<built-in function len>,
)
```
   - chunk_overlap: a little overlap between two chunks. allows for the same piece of context to be at the end of one chunk and at the start of another chunk. It helps create some notion of consistency
4. The text splitters in LangChain all have a create documents and a split documents method. This involves the same logic under the hood, it just exposes a slightly different interface. One that takes in a list of text and another takes in a list of documents.

Methods:

create_documents() - Create documents from a list of texts

split_documents() - split documents

5. Types of splitters (lists a few of them)
   - CharacterTextSplitter()
   - MarkdownHeaderTextSplitter()
   - TokenTextSplitter()
   - SentenceTransformersTokenTextSplitter()
   - RecursiveCharacterTextSplitter(): Implementation of splitteing text that looks at characters. Recursively tries to split by different characters to find one that works.
   - Language(): for CPP, Python, Ruby, Markdwon etc

# Vectorstores and Embedding 
1. Embeddings
   - Embedding vector captures content/meaning
   - Text with similar content will have similar vectors
   - We can compare those vectors to find pieces of texts that are similar
2. Vector store
   - is a database where you can easily look up similar vectors later on.
   - This will become useful where we're trying to find documents that are relevant for a question at hand.
![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/blob/eace526aa4ab9764d9cd976a715b4171f625a582/VectorStore.png)
   - We can then take the question at hand, create an embedding, and then do comparisons to all the different vectors in the vector store, and then pick the n most similar.
   - We then take those n most similar chunks, and pass them along with the question into an LLM, an get back an answer
![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/blob/2840aa8cb3fb93f0b21a9232d0de19639501a239/VectorStore_and_Database.png)

# Retrieval
1. Retrieval is important at query time, when you've got a query that comes in and you want to retrieved the most relevant splits.
2. Retrieval
   - Accessing/indexing the data in the vector store
     + Basic semantic similarity
     + Maximum marginal relevance
     + Including Metadata
   - LLM Aided Retrieval
3. Maximum marginal relevance (MMR)
   - you may not always want to choose the most similar responses

![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/assets/151610467/333b2a73-3b73-452f-841f-9bb46d78b06e)

4. MMR algorithm
   - query the vector store
   - choose the 'fetch_k' most similar responses
   - within those responses choose the 'k' most diverse
5. LLM Aided Retrieval
   - There are several situations where the query applied to the database is more than just the quesiton asked
   - One is SelfQuery, where we use an LLM to convert the user question into a query
![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/blob/dcee8c7adff177a69f912b5b9a95abf1405454cc/LLM_Aided_Retrieval.png)
6. Compression
   - Increase the number of results you can put in the context by shrinking the responses to only the relevant information
![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/blob/57207de7ffc4d6672ccf54c168dcbbb342adc8d0/screenshots/Compression.png)
7. Other types of retrieval
   - Not using a vector database, such as:
     + SVM
     + TF-IDF
     + ...

## Question Answering
1. Question Answering
   - Multiple relevant documents have been retrieved from the vector store
   - Potentially compress the relevant splits to fit into the LLM context
   - Send the information along with out question to an LLM to select and format an answer
2. RetrievalQA chain

![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/assets/151610467/8cb86669-3794-410a-95f9-7059d6bbd934)

3. 3 additional methods: Sometimes there's can be a lot of documents, that you can't pass them all into the same context window.
   - Map_reduce
   - Refine
   - Map_rerank

![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/assets/151610467/0bdcc2e3-48d1-403a-92ca-f101a8b4e700)

## Question Answering ChatBot
![image](https://github.com/FionaYuY/LangChain_chat_with_your_data_notes/assets/151610467/894e2474-d8c7-47f7-848f-2aa5f3216a69)

1. chat history

```
from langchain.memory import ConversationBufferMemory
memory = ConversationBufferMemory(
   memory_key = 'chat_history',
   return_messages = True
)
```




