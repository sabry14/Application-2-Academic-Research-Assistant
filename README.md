# Academic Research Assistant System

## Overview
The Academic Research Assistant is a Python-based system designed to streamline academic research by collecting, filtering, and synthesizing information from sources such as ArXiv and Wikipedia. It leverages **LangChain**, **FAISS**, and **OpenAI's GPT models** to provide relevant insights and formatted research reports.

## Features
- **Automated Research Collection**: Fetch data from ArXiv and Wikipedia.
- **Relevance Filtering**: Uses FAISS and sentence embeddings to filter relevant documents.
- **AI-Powered Synthesis**: Generates formatted academic reports (e.g., APA style).
- **Citation Tracking**: Maintains a list of research sources used.

## Prerequisites
Ensure you have the following installed:
- Python 3.7+
- Required libraries:

```bash
pip install -U langchain-community arxiv wikipedia langchain-openai faiss-cpu sentence-transformers
```

## Setup Instructions
1. **Clone the Repository** (if applicable)
   ```bash
   git clone https://github.com/your-repo/academic-research-assistant.git
   cd academic-research-assistant
   ```

2. **Install Dependencies**
   ```bash
   pip install -U langchain-community arxiv wikipedia langchain-openai faiss-cpu sentence-transformers
   ```

3. **Set Up OpenAI API Key**
   Obtain an OpenAI API key from [OpenAI](https://platform.openai.com/signup) and set it as an environment variable:
   ```bash
   export OPENAI_API_KEY="your_openai_api_key"
   ```
   Or modify the script directly:
   ```python
   self.llm = ChatOpenAI(model="gpt-3.5-turbo", temperature=0.3, openai_api_key="your_openai_api_key")
   ```

## Usage Example

```python
from academic_research_assistant import AcademicResearchAssistant

# Initialize assistant
assistant = AcademicResearchAssistant()

# Conduct research on quantum computing in cryptography
research_data = assistant.research(
    "quantum computing applications in cryptography",
    tools=["arxiv", "wikipedia"]
)

# Filter relevant information
documents = [research_data["arxiv"], research_data["wikipedia"]]
relevant_docs = assistant.filter_relevant(
    documents, "post-quantum cryptography algorithms", threshold=0.65
)

# Generate a formatted research report
report = assistant.synthesize({"relevant_docs": relevant_docs}, format="APA")

print("# Academic Research Report\n")
print(report)

print("\n## Research Sources\n")
for i, source in enumerate(assistant.sources, 1):
    print(f"{i}. {source['tool'].title()}: {source['query']}")
```

## Expected Output
- **Formatted Research Report** in APA citation style.
- **List of Sources** used in the research.

## Troubleshooting
- **API Key Error**: Ensure your API key is set correctly.
- **Rate Limit Error (429)**: Check OpenAI usage limits at [OpenAI Dashboard](https://platform.openai.com/account/usage).
- **Missing Dependencies**: Run `pip install -U <package_name>` to ensure all required libraries are installed.

## Future Enhancements
- Support for more data sources (Google Scholar, PubMed, etc.).
- Advanced citation formats (MLA, Chicago).
- Improved document summarization using LLM fine-tuning.

---

Developed by [Your Name] | [Your Contact Info]

