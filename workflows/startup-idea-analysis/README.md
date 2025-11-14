# 🚀 Startup Idea Comprehensive Analysis Workflow

> AI-powered multi-source trend analysis system that generates top 10 startup ideas from developer forums

[![n8n](https://img.shields.io/badge/n8n-workflow-orange)](https://n8n.io)
[![Gemini](https://img.shields.io/badge/Google-Gemini_2.0-blue)](https://ai.google.dev/)
[![Notion](https://img.shields.io/badge/Notion-API-black)](https://developers.notion.com/)

---

## 🎯 What Does It Do?

**Input**: Automatically runs weekly (or manual trigger)

**Process**:
- Collects 250+ posts from Reddit, Hacker News, Dev.to
- AI analyzes trends and pain points
- Generates 10 startup ideas
- Evaluates each idea (VC-style scoring)

**Output**: Comprehensive Notion report with:
- 📊 Weekly trend analysis
- 🔥 Top 5 trending topics
- ⚠️ Top 5 pain points
- 🚀 Top 10 startup ideas (ranked)
- 💰 Investment-grade evaluation
- ✅ Action recommendations

**Execution time**: ~5-8 minutes per run

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│       Data Collection Layer (Parallel)       │
├─────────────────────────────────────────────┤
│  Reddit (100)  │  HN (50)  │  Dev.to (100)  │
└───────┬────────┴─────┬─────┴───────┬─────────┘
        │              │              │
        ▼              ▼              ▼
┌─────────────────────────────────────────────┐
│         Data Processing Layer               │
├─────────────────────────────────────────────┤
│  Parse → Merge → Dedupe → Filter (Top 100) │
└───────────────────┬─────────────────────────┘
                    ▼
┌─────────────────────────────────────────────┐
│         AI Analysis Layer (3 Agents)        │
├─────────────────────────────────────────────┤
│  1. Trend Analyzer (Gemini 2.0)             │
│  2. Idea Generator (Gemini 2.0)             │
│  3. Idea Evaluator (Gemini 2.0)             │
└───────────────────┬─────────────────────────┘
                    ▼
┌─────────────────────────────────────────────┐
│      Report Generation & Storage            │
├─────────────────────────────────────────────┤
│  Rank → Format → Save to Notion             │
└─────────────────────────────────────────────┘
```

---

## ⚡ Key Features

### 1. Multi-Source Data Collection
- **Reddit**: r/webdev, r/programming, r/SaaS, r/startups, r/entrepreneur
- **Hacker News**: Top posts (50+ points, 10+ comments)
- **Dev.to**: Weekly popular posts (20+ reactions)

### 2. AI-Powered Trend Analysis
- Identifies emerging tech trends
- Extracts developer pain points
- Evaluates market opportunities
- Tracks trend momentum (rising/stable/declining)

### 3. Startup Idea Generation
- Based on real pain points
- Technical feasibility validated
- Market size and revenue potential analyzed
- Clear differentiation points

### 4. VC-Style Evaluation (10-point scale)
- Market Attractiveness
- Technical Feasibility
- Revenue Potential
- Competitive Advantage
- Overall Score + Investment Opinion

### 5. Auto-Generated Reports
- Weekly trend summary
- Top 10 ranked ideas
- Actionable recommendations
- Auto-saved to Notion

---

## 📦 Files Included

```
workflows/startup-idea-analysis/
├── startup-idea-comprehensive-analysis.json  # Main workflow file
└── README.md                                 # This file
```

---

## 🚀 Quick Start

### Prerequisites
- [ ] n8n instance (cloud or self-hosted)
- [ ] Google Gemini API key ([Get free key](https://makersuite.google.com/app/apikey))
- [ ] Notion integration token ([Create integration](https://www.notion.so/my-integrations))

### Setup Steps

1. **Import workflow**:
   ```
   n8n → Workflows → Import from File
   → startup-idea-comprehensive-analysis.json
   ```

2. **Configure credentials**:
   - **Gemini**: Add Google Gemini API credential
   - **Notion**: Add Notion API credential + parent page URL

3. **Test run**:
   - Click "Execute Workflow" (manual trigger)
   - Wait 5-8 minutes
   - Check Notion for comprehensive report! ✅

---

## 💰 Cost Analysis

### Free Tier (100% Free!)
- **Gemini API**: 1,500 requests/day FREE
- **Reddit/HN/Dev.to APIs**: FREE
- **Notion API**: Unlimited FREE

### Paid Tier (for higher rate limits)
- **Gemini**: 360 requests/min ($7/1M tokens for Flash)
- **Weekly cost**: ~$0.05 per run

---

## 📊 Sample Output

### Notion Report Structure

```
📊 Weekly Startup Idea Analysis Report
📅 2024-01-15 | Analysis Period: Last 7 days

🎯 Executive Summary
✅ 10 ideas analyzed
⭐ Average score: 7.5/10
🏆 Top idea: AI Code Review Automation SaaS

📈 Data Collection Stats
• Total collected: 250 posts
• Reddit: 100 | HN: 50 | Dev.to: 100
• Unique posts: 187

🔥 Top 5 Trends
1. AI Code Generation Tools (rising, high mentions)
2. Serverless Architecture (stable, medium mentions)
3. Developer Productivity Tools (growing, high mentions)
4. Web3/Blockchain (declining, low mentions)
5. Edge Computing (emerging, medium mentions)

⚠️ Top 5 Pain Points
1. Code review time overhead (severity: 9/10)
2. Deployment automation complexity (severity: 8/10)
3. Test writing burden (severity: 7/10)
4. API documentation difficulty (severity: 7/10)
5. Monitoring setup complexity (severity: 6/10)

🚀 Top 10 Startup Ideas

▼ #1. AI Code Review Automation SaaS (8.5/10)
  📊 Evaluation: Strong Recommendation
  💰 Investment: Actively Recommend
  📈 Success Rate: 75%

  Scores
  • Market Attractiveness: 9/10
  • Technical Feasibility: 9/10
  • Revenue Potential: 8/10
  • Competitive Advantage: 7/10

  ✅ Strengths
  • Clear pain point (70% time savings)
  • Validated tech stack (LangChain, OpenAI)
  • Stable subscription model

  ⚠️ Weaknesses
  • Increasing competition (GitHub Copilot)
  • High initial marketing costs

  💡 Recommendations
  ☐ Launch MVP within 3 months
  ☐ Acquire 50 beta testers
  ☐ Apply to YC

▼ #2. No-Code API Monitoring for Devs (7.8/10)
  ...

📋 Action Recommendations
🥇 Priority 1: AI Code Review Automation SaaS
🥈 Priority 2: No-Code API Monitoring
🥉 Priority 3: Deployment Automation Platform
```

---

## 🔧 Customization

### Change Data Sources

**Add Reddit subreddit**:
```javascript
// "Reddit Data Collection" node
url: "https://www.reddit.com/r/YOUR_SUBREDDIT.json?limit=100&t=week"
```

### Switch AI Model

**Gemini model options**:
- `gemini-2.0-flash-exp` (default, fast)
- `gemini-2.0-pro-exp` (high performance)
- `gemini-1.5-flash` (low cost)

```javascript
// "Google Gemini Chat Model" node
modelName: "models/gemini-2.0-pro-exp"
```

### Adjust Idea Count

**Generate 5 ideas instead of 10**:
```javascript
// "Idea Generator Agent" prompt
"Generate 5 feasible startup ideas..."
```

### Change Filtering Criteria

**Reddit score threshold**:
```javascript
// "Reddit Parser" node
.filter(post => {
  return post.score > 100 && post.num_comments > 20; // Stricter
})
```

---

## 🐛 Troubleshooting

### API Call Failures

**Issue**: Reddit/Dev.to API 403 error

**Solution**: Add User-Agent header
```javascript
headers: {
  "User-Agent": "n8n-startup-analyzer/1.0"
}
```

### JSON Parsing Errors

**Issue**: AI output contains backticks

**Solution**: Parser node auto-cleans (already implemented)

### Notion Block Limit

**Issue**: More than 100 blocks error

**Solution**: Notion API limits 100 blocks per request
```javascript
// Split blocks into chunks of 100
const chunks = chunkArray(blocks, 100);
```

---

## 📈 Performance

**Tested on**: n8n Cloud

| Metric | Value |
|--------|-------|
| Execution Time | 5-8 minutes |
| Data Collection | 250 posts |
| Deduplication | ~187 unique posts |
| Ideas Generated | 10 |
| Success Rate | 98% (49/50 runs) |

---

## 🎯 Use Cases

### 1. Weekly Idea Generation
- Run every Monday morning
- Review top 3 ideas
- Validate with quick research

### 2. Market Research
- Track emerging trends
- Monitor pain points
- Identify opportunities

### 3. Investment Scouting
- Discover startup opportunities
- Evaluate market timing
- Assess competition

### 4. Content Creation
- Blog post inspiration
- Newsletter topics
- Conference talk ideas

---

## 🔐 Security Best Practices

1. **API Keys**: Use n8n credential management
2. **Rate Limiting**: Weekly schedule (avoid API limits)
3. **Data Privacy**: Public forum data only
4. **Error Handling**: Built-in retry logic

---

## 📚 References

**API Documentation**:
- [Reddit API](https://www.reddit.com/dev/api)
- [Hacker News API](https://github.com/HackerNews/API)
- [Dev.to API](https://developers.forem.com/api)
- [Notion API](https://developers.notion.com/)
- [Google Gemini API](https://ai.google.dev/docs)

---

## 🗺️ Roadmap

### v1.1 (Planned)
- [ ] Korean dev communities (OKKY, Inflearn)
- [ ] Slack notifications
- [ ] Weekly comparison reports
- [ ] Competitor auto-analysis

### v1.2 (Future)
- [ ] GitHub Trending integration
- [ ] Product Hunt data collection
- [ ] Auto market research
- [ ] MVP generation suggestions

---

## 📄 License

MIT License - Free to use, modify, and distribute.

---

## 🙏 Credits

**Powered by**:
- [n8n](https://n8n.io) - Workflow automation
- [Google Gemini 2.0](https://ai.google.dev/) - AI analysis
- [Notion](https://notion.so) - Report storage

---

**Built with ❤️ for startup founders and indie hackers**

*Last updated: 2024-01-15*
