# AI Query-Based Image Finder

## 🤔 The Missing Piece in LLM Conversations

After working with OpenAI, Claude, Gemini, and other major LLM providers, there's a **critical gap** that nobody talks about:

### What LLMs Excel At:
✅ Intelligent text responses  
✅ Code generation  
✅ Complex reasoning  
✅ AI-generated images (DALL-E, Midjourney)  
✅ Web search integration (some models)  

### The Blind Spot:
❌ **Real image retrieval from the web**

Think about it - when you ask ChatGPT:
> *"Show me images of the new Tesla Cybertruck interior and worthy to buy or not"*

You get:
- "I can't browse for images"
- "Try searching Google Images"  
- "I can generate an AI version"
- Text descriptions only

**But what if you need REAL images?**

📸 Authentic product photos  
📸 Historical documentation  
📸 Current event visuals  
📸 Research materials  
📸 Marketing assets  

## 🚀 How It Works

1. **Query Analysis**: LangChain analyzes the user query to determine if images would enhance the response
2. **Image Search**: If needed, Apify Actor searches Google Images using multiple search perspectives
3. **Enhanced Response**: LangChain generates a comprehensive response incorporating the visual context

## 📋 Prerequisites

- Python 3.7+
- Google API Key (for Gemini model)
- Apify API Token

## 🛠️ Installation

### 1. Clone the Repository


### 2. Create Virtual Environment
```bash
python -m venv venv
```

### 3. Activate Virtual Environment

**Windows (PowerShell):**
```powershell
.\venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```cmd
venv\Scripts\activate
```

**macOS/Linux:**
```bash
source venv/bin/activate
```

### 4. Install Dependencies
```bash
pip install -r requirements.txt
```

## 🔧 Configuration

### API Keys Setup

1. **Google API Key**: Get your API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
2. **Apify Token**: Get your token from [Apify Console](https://console.apify.com/account/integrations)

### Update API Keys in Code

Edit `main.py` and replace the placeholder values:

```python
assistant = LangChainApifyAssistant(
    gemini_key="your_google_api_key_here",  # Replace with actual Google API key
    apify_token="your_apify_token_here"     # Replace with actual Apify token
)
```

## 💻 Usage

### Basic Usage

```python
from main import LangChainApifyAssistant

# Initialize the assistant
assistant = LangChainApifyAssistant(
    gemini_key="your_google_api_key",
    apify_token="your_apify_token"
)

# Process a query
result = assistant.process_query("Tesla Model Y interior dashboard")

# Access the results
print(result['text_response'])  # Image-aware text response
print(f"Found {result['total_images']} images")
print(f"Search perspectives: {len(result['perspectives'])}")
```

### Running the Demo

```bash
python main.py
```

The demo will showcase:
- Text-only responses for general queries
- Image-enhanced responses for visual queries

## 📊 Response Structure

The `process_query` method returns a dictionary with:

```python
{
    'query': str,                    # Original user query
    'text_response': str,            # Generated text response
    'images': list,                  # List of found images with metadata
    'total_images': int,             # Total number of images found
    'perspectives': list,            # Search perspectives used
    'image_aware_response': bool     # Whether images influenced the response
}
```

