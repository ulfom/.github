# Ulfom

![Version](https://img.shields.io/badge/version-beta-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)

> Turn messy web content into clean, useful data

## 🚀 Overview

Ulfom is a powerful API that helps developers and AI teams automatically collect, clean, and organize web content in structured formats. Stop wrestling with messy HTML and inconsistent data formats - Ulfom handles the hard parts for you.

## ✨ Key Features

- **Structured Content Extraction** - Convert web content into structured data using custom JSON schemas and AI processing
- **Async Processing** - Handle large-scale content processing with our efficient async task system
- **Smart Crawling** - Intelligent sitemap and recursive crawling with built-in rate limiting and error handling

## 🔍 Use Cases

### Markdown Processing
Convert web content into clean, readable markdown format. Perfect for:
- Content management systems
- Documentation generators
- AI training data preparation
- Knowledge base creation

### AI Content Analysis
Extract structured information using custom schemas. Ideal for:
- Market research automation
- Competitive analysis
- Content categorization
- Automated data extraction

### Intelligent Web Crawling
Smart, efficient web content collection. Perfect for:
- Content aggregation
- Website migration
- Documentation archival
- SEO analysis

## 📦 Installation

```bash
pip install ulfom
```

## 🔑 Authentication

To use the Ulfom API, you'll need an API key. Sign up at [ulfom.com](https://www.ulfom.com) to get your key.

```python
from ulfom import UlfomClient

# Initialize with your API key
client = UlfomClient(api_key="your_api_key_here")
```

## 💻 Quick Start

### Structured Content Processing

```python
import asyncio
from ulfom import UlfomClient

async def process_content():
    client = UlfomClient()
    
    # Create a structured processing task
    task_id = await client.create_task(
        service="structured_task",
        url="https://example.com/article",
        parameters={
            "prompt": "Extract key information",
            "json_schema": {
                "type": "object",
                "properties": {
                    "title": {"type": "string"},
                    "main_points": {"type": "array", "items": {"type": "string"}},
                    "summary": {"type": "string"}
                }
            }
        }
    )
    
    # Wait for results
    result = await client.wait_for_result(task_id)
    print(result)

asyncio.run(process_content())
```

### Sitemap Crawling

```python
import asyncio
from ulfom import UlfomClient

async def crawl_site():
    client = UlfomClient()
    
    # Create a sitemap crawl task
    task_id = await client.create_task(
        service="sitemap_crawl",
        url="https://example.com",
        parameters={
            "concurrent_requests": 5,
            "max_pages": 1000,
            "output_format": "markdown"
        }
    )
    
    # Check status periodically
    while True:
        status = await client.get_task_status(task_id)
        print(f"Progress: {status['progress']}%")
        
        if status['status'] == 'completed':
            result = await client.get_task_result(task_id)
            print(f"Crawled {len(result['pages'])} pages")
            break
            
        await asyncio.sleep(5)

asyncio.run(crawl_site())
```

## 📚 API Reference

### Task Creation

```bash
curl -X POST "https://api.ulfom.com/task/structured_task" \
    -H "Authorization: Bearer YOUR_API_KEY" \
    -H "Content-Type: application/json" \
    -d '{
        "url": "https://example.com/article",
        "parameters": {
            "prompt": "Extract key points and conclusions",
            "json_schema": {
                "type": "object",
                "properties": {
                    "key_points": {"type": "array", "items": {"type": "string"}},
                    "conclusion": {"type": "string"}
                }
            }
        }
    }'
```

### Available Endpoints

| Endpoint | Description |
|----------|-------------|
| `/task/structured_task` | Extract structured data from a URL using JSON schema |
| `/task/sitemap_crawl` | Crawl a website using its sitemap |
| `/task/recursive_crawl` | Crawl a website recursively following links |
| `/task/status/:id` | Check the status of an existing task |
| `/task/result/:id` | Retrieve the result of a completed task |

## 🤝 Integration Scenarios

Ulfom provides flexible integration options for various use cases:
- LLM training data preparation
- Knowledge base enrichment
- Content recommendation systems
- Research and analysis platforms

## 📄 Examples

Check out our [examples directory](./examples) for more detailed implementation examples.

## 📝 Documentation

For comprehensive documentation, visit [docs.ulfom.com](https://docs.ulfom.com).

## 🔐 Security

We take security seriously. Ulfom:
- Uses HTTPS for all API communications
- Implements rate limiting to prevent abuse
- Provides secure API key management
- Respects robots.txt and crawl delay directives

## 🤔 Support

- [Documentation](https://docs.ulfom.com)
- [Example Code](https://github.com/ulfom/examples)
- [Issue Tracker](https://github.com/ulfom/ulfom/issues)
- [Discord Community](https://discord.gg/ulfom)

## 📊 Roadmap

- [ ] Advanced content filtering
- [ ] Custom AI model integration
- [ ] Webhook notifications
- [ ] Real-time content monitoring
- [ ] Enhanced schema validation
