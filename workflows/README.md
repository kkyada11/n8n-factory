# 🏭 n8n Workflows Collection

> Production-ready n8n workflows for AI-powered automation

[![n8n](https://img.shields.io/badge/n8n-workflows-orange)](https://n8n.io)
[![Workflows](https://img.shields.io/badge/workflows-2-brightgreen)]()
[![License](https://img.shields.io/badge/license-MIT-blue)]()

---

## 📚 Available Workflows

### 1. 🔬 Design Pattern Deep Research

**Location**: [`design-pattern-research/`](./design-pattern-research/)

Automated research system that generates comprehensive Notion documentation for any React/JavaScript design pattern.

**Features**:
- 🔍 Google search with AI-optimized queries
- 🌐 Intelligent web scraping (5 authoritative sources)
- 🤖 Dual AI analysis (content + code generation)
- 📝 Auto-generated Notion pages with structured content

**Tech Stack**: Google Gemini API, SerpAPI, Notion API, cheerio

**Execution Time**: 60-90 seconds

**Use Cases**: Learning new technologies, team documentation, content creation

👉 **[View Details](./design-pattern-research/README.md)**

---

### 2. 🚀 Startup Idea Comprehensive Analysis

**Location**: [`startup-idea-analysis/`](./startup-idea-analysis/)

Multi-source trend analysis system that generates top 10 VC-evaluated startup ideas from developer forums.

**Features**:
- 📊 Multi-source data collection (Reddit, HN, Dev.to)
- 🔥 AI trend analysis and pain point extraction
- 💡 10 startup ideas with market validation
- 🎯 Investment-grade evaluation (10-point scale)
- 📋 Comprehensive weekly reports in Notion

**Tech Stack**: Google Gemini 2.0, Reddit API, Hacker News API, Dev.to API, Notion API

**Execution Time**: 5-8 minutes

**Use Cases**: Idea generation, market research, investment scouting

👉 **[View Details](./startup-idea-analysis/README.md)**

---

## 🚀 Quick Start

### Prerequisites

All workflows require:
- ✅ n8n instance (cloud or self-hosted)
- ✅ Google Gemini API key ([Get free key](https://makersuite.google.com/app/apikey))
- ✅ Notion integration token ([Create integration](https://www.notion.so/my-integrations))

### Installation Steps

1. **Choose a workflow** from the list above
2. **Navigate** to its directory
3. **Read** the specific README for detailed setup
4. **Import** the JSON file to n8n
5. **Configure** API credentials
6. **Execute** and enjoy automation! 🎉

---

## 📊 Workflows Comparison

| Feature | Design Pattern Research | Startup Idea Analysis |
|---------|------------------------|----------------------|
| **Execution Time** | 60-90 seconds | 5-8 minutes |
| **AI Agent Count** | 2 (analysis + code) | 3 (trend + idea + eval) |
| **Data Sources** | Google Search | Reddit, HN, Dev.to |
| **Output Format** | Single Notion page | Comprehensive report |
| **Use Case** | Technical learning | Business ideation |
| **Cost (Free Tier)** | 33/month | Unlimited |
| **Complexity** | Medium | High |

---

## 🔧 Common Setup

### 1. Google Gemini API

**All workflows use Gemini for AI processing.**

**Setup**:
1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Click "Create API Key"
3. Copy the key (starts with `AIza...`)
4. Add to n8n credentials as "Google Gemini API"

**Free Tier**: 15 requests/minute, 1500 requests/day

---

### 2. Notion API

**All workflows save results to Notion.**

**Setup**:
1. Visit [Notion Integrations](https://www.notion.so/my-integrations)
2. Click "New integration"
3. Name it "n8n Automation Bot"
4. Copy "Internal Integration Token"
5. **Share your target page** with this integration
6. Copy the page ID from URL:
   ```
   https://www.notion.so/workspace/PAGE_ID?...
                                 ^^^^^^^^^ (32 chars)
   ```

**Free Tier**: Unlimited requests

---

## 📁 Directory Structure

```
workflows/
├── README.md                          # This file (index)
│
├── design-pattern-research/
│   ├── design-pattern-research-workflow.json
│   ├── README.md                      # Workflow details
│   └── SETUP-GUIDE.md                 # Detailed setup
│
└── startup-idea-analysis/
    ├── startup-idea-comprehensive-analysis.json
    └── README.md                      # Workflow details
```

---

## 🎯 Recommended Learning Path

### Beginner
**Start here**: Design Pattern Research
- Simpler workflow (2 AI agents)
- Shorter execution time
- Clear input/output
- Learn: Web scraping, AI prompting, Notion API

### Intermediate
**Next step**: Startup Idea Analysis
- Complex multi-source data collection
- Advanced AI agent orchestration
- Learn: Parallel processing, data deduplication, structured analysis

---

## 🔐 Best Practices

### 1. API Key Management
- ✅ Use n8n's built-in credential management
- ❌ Never hardcode keys in workflow JSON
- ✅ Use environment variables for production

### 2. Rate Limiting
- Add "Wait" nodes between API calls
- Respect free tier limits
- Monitor usage in API dashboards

### 3. Error Handling
- Enable error workflows
- Add retry logic for network failures
- Log errors to monitoring service

### 4. Cost Optimization
- Use Gemini Flash (90% cheaper than GPT-4)
- Schedule workflows during off-peak hours
- Cache results when possible

---

## 🐛 Common Issues

### Issue: "cheerio is not defined"

**Workflows affected**: Design Pattern Research

**Solution**:
```bash
# Self-hosted n8n
docker exec -it n8n npm install cheerio
```

### Issue: Gemini rate limit exceeded

**Workflows affected**: All

**Solution**:
- Add 10-second "Wait" node between Gemini calls
- Or upgrade to paid tier

### Issue: Notion "validation_error"

**Workflows affected**: All

**Solution**:
- Verify integration is shared with target page
- Check page ID is correct (32 characters)
- Ensure all text fields are strings

---

## 🗺️ Roadmap

### Upcoming Workflows

- [ ] **AI Meeting Summarizer** - Transcribe → Summarize → Action Items
- [ ] **GitHub Issue Triager** - Auto-label, prioritize, assign
- [ ] **Content Repurposing Engine** - Blog → Twitter thread → LinkedIn post
- [ ] **Competitor Tracker** - Monitor pricing, features, announcements
- [ ] **Code Review Automator** - Analyze PRs, suggest improvements

**Vote for next workflow**: [Open an issue](https://github.com/kkyada11/n8n-factory/issues)

---

## 🤝 Contributing

Have improvements? Found a bug?

1. Test changes with 3+ different inputs
2. Update README if workflow changes
3. Document new nodes
4. Share your workflow!

**Contribution ideas**:
- Add new data sources
- Optimize AI prompts
- Improve error handling
- Translate documentation
- Create video tutorials

---

## 📄 License

MIT License - Free to use, modify, and distribute.

**Attribution**: If you share publicly, please credit this repository.

---

## 📞 Support

**Need help?**
1. Check individual workflow READMEs
2. Review n8n execution logs
3. Test nodes individually (right-click → Execute Node)
4. Open an issue in this repository

**Questions or feedback?**
- Open an issue
- Share your success stories!
- Suggest new workflows

---

## 🙏 Acknowledgments

**Built with**:
- [n8n](https://n8n.io) - Workflow automation platform
- [Google Gemini](https://ai.google.dev/) - AI/LLM API
- [Notion](https://notion.so) - Documentation & knowledge base

**Inspired by**: The n8n community and real-world automation needs

---

**Built with ❤️ for the automation community**

*Last updated: 2025-11-14*
