# Quick Reference: Common Gen AI Tasks

This is a quick reference guide for common tasks you might need help with while working through the Gen AI training materials.

## 🔧 Setup & Configuration

### API Setup Issues
**Problem**: "My API calls aren't working"
- Check API key configuration
- Verify project ID and region settings
- Ensure proper authentication
- Validate endpoint URLs

### Notebook Environment
**Problem**: "Dependencies not found"
- Install required packages: `!pip install google-cloud-aiplatform`
- Check Python version compatibility
- Restart kernel after installations

## 💡 Prompt Engineering Quick Tips

### Make Prompts More Effective
```python
# Instead of:
prompt = "Summarize this text"

# Try:
prompt = """Summarize the following text in 2-3 sentences, focusing on the main points:

Text: {your_text}

Summary:"""
```

### Add Context and Constraints
```python
prompt = """You are a helpful assistant for technical documentation.
Rules:
- Keep responses concise
- Use bullet points for lists
- Include code examples when relevant

Question: {user_question}"""
```

## 🐛 Common Error Fixes

### Rate Limiting
```python
import time
from google.api_core import retry

# Add retry logic
@retry.Retry(deadline=60)
def call_model_with_retry(prompt):
    return model.generate_content(prompt)
```

### Token Limits
```python
# Check input length
if len(prompt) > max_tokens:
    prompt = prompt[:max_tokens]
```

### JSON Parsing Errors
```python
import json
import re

def extract_json(response_text):
    # Find JSON in response
    json_match = re.search(r'```json\n(.*?)\n```', response_text, re.DOTALL)
    if json_match:
        return json.loads(json_match.group(1))
    return None
```

## 📊 Model Parameter Tuning

### For Creative Tasks
```python
generation_config = {
    "temperature": 0.8,  # Higher for creativity
    "top_p": 0.9,
    "max_output_tokens": 1024
}
```

### For Factual Tasks
```python
generation_config = {
    "temperature": 0.1,  # Lower for consistency
    "top_p": 0.8,
    "max_output_tokens": 512
}
```

## 🎯 Task-Specific Tips

### Text Summarization
- Use clear length constraints: "in 50 words" or "in 3 bullet points"
- Specify summary type: "executive summary", "key points", "abstract"

### Question Answering
- Include context: "Based on the provided context, answer the question"
- Handle unknowns: "If the answer isn't in the context, say 'Information not available'"

### Text Classification
- Provide clear categories and examples
- Use few-shot prompting with 2-3 examples per category

### Text Extraction
- Specify exact output format (JSON, CSV, etc.)
- Include field definitions and examples

## 🚨 When to Ask for Help

Ask for assistance when you encounter:
- Unexpected model outputs or hallucinations
- Performance issues or slow responses
- Complex prompt engineering challenges
- Integration problems with APIs
- Code optimization needs
- Unclear error messages

## 📞 How to Ask for Help

Be specific in your questions:
- Include relevant code snippets
- Describe expected vs actual behavior
- Share error messages
- Mention which notebook/task you're working on

**Example**: "I'm working on the text classification notebook and getting inconsistent results. Here's my prompt: [code]. The model sometimes returns the wrong format. How can I make it more reliable?"