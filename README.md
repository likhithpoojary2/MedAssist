# MedAssist - Medical Chatbot

A Flask-based medical chatbot application that provides reliable health information using RAG (Retrieval-Augmented Generation) technology. The application uses Google's Gemini AI model and Pinecone vector database to answer medical queries based on provided medical documentation.

## Features

- **Medical Information Chatbot**: Interactive web interface for medical queries
- **RAG Implementation**: Retrieval-Augmented Generation for accurate responses
- **PDF Document Processing**: Extracts and processes medical PDF documents
- **Vector Database**: Uses Pinecone for efficient document retrieval
- **Modern UI**: Clean, responsive chat interface with loading animations

## Technology Stack

- **Backend**: Flask (Python web framework)
- **AI Model**: Google Gemini 2.5 Flash
- **Vector Database**: Pinecone
- **Embeddings**: HuggingFace sentence-transformers (all-MiniLM-L6-v2)
- **Document Processing**: LangChain with PyPDF
- **Frontend**: HTML, CSS, JavaScript

## Project Structure

```
MedAssist/
├── app.py                 # Main Flask application
├── store_index.py         # Script to create and populate Pinecone index
├── requirements.txt       # Python dependencies
├── setup.py              # Package setup configuration
├── template.py           # Project structure template generator
├── test.py               # Test file (empty)
├── src/
│   ├── __init__.py
│   ├── helper.py         # PDF processing and embedding utilities
│   └── prompt.py         # System prompt configuration
├── templates/
│   └── chat.html         # Chat interface template
├── static/
│   ├── chat.css          # Styling for chat interface
│   └── logo.jpg          # Application logo
├── Data/
│   └── Medical_book.pdf  # Medical reference document
├── research/
│   └── trials.ipynb      # Research and development notebook
└── env/                  # Virtual environment directory
```

## Prerequisites

- Python 3.x
- Pinecone API key
- Google API key (for Gemini AI)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd MedAssist
```

2. Create and activate virtual environment:
```bash
python -m venv env
# On Windows
env\Scripts\activate
# On macOS/Linux
source env/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Set up environment variables:
Create a `.env` file in the root directory with:
```
PINECONE_API_KEY=your_pinecone_api_key
GOOGLE_API_KEY=your_google_api_key
```

## Setup Vector Database

1. Run the index creation script:
```bash
python store_index.py
```

This script will:
- Load the medical PDF from the `Data/` directory
- Split the document into text chunks
- Create embeddings using HuggingFace model
- Store embeddings in Pinecone vector database

## Running the Application

Start the Flask application:
```bash
python app.py
```

The application will be available at `http://localhost:8080`

## How It Works

1. **Document Processing**: The system loads medical PDF documents and splits them into manageable text chunks
2. **Embedding Generation**: Text chunks are converted to vector embeddings using HuggingFace's sentence-transformers
3. **Vector Storage**: Embeddings are stored in Pinecone vector database for efficient retrieval
4. **Query Processing**: When a user asks a question:
   - The query is converted to embeddings
   - Similar documents are retrieved from Pinecone
   - Context is provided to Google Gemini AI
   - AI generates a response based on the retrieved medical information

## API Endpoints

- `GET /`: Serves the chat interface
- `POST /get`: Processes chat messages and returns AI responses

## System Prompt

The chatbot is configured with a medical assistant system prompt that:
- Provides reliable health information based on retrieved context
- Limits responses to three sentences for conciseness
- Recommends consulting healthcare professionals when information is not available
- Maintains professional and accurate medical communication

## Dependencies

- `sentence-transformers==2.2.2`: For text embeddings
- `langchain`: For RAG implementation
- `flask`: Web framework
- `pypdf`: PDF document processing
- `python-dotenv`: Environment variable management
- `pinecone[grpc]`: Vector database
- `langchain-pinecone`: Pinecone integration
- `langchain_google_genai`: Google Gemini AI integration

## Development

The project includes a research notebook (`research/trials.ipynb`) for experimentation and development. The `template.py` file can be used to generate the project structure for new installations.

## License

This project is licensed under the terms specified in the LICENSE file.

## Author

- **Author**: likhith
- **Email**: likhithan02@gmail.com
