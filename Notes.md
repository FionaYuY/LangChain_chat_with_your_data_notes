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
3. Document loading -> splitting -> storage

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


