# Design Pattern Research Workflow - Setup Guide

## 📋 Overview

This n8n workflow automatically researches a React design pattern and creates a comprehensive Notion page with:
- Overview and key concepts
- Advantages and disadvantages
- Real-world use cases
- Step-by-step setup guide
- Working TypeScript code example
- Source URLs

**Execution time**: ~60-90 seconds per pattern

---

## 🔑 Required API Keys

### 1. Google Gemini API
**Purpose**: Generate optimized search queries, analyze content, generate code

**How to get**:
1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Click "Create API Key"
3. Copy the key (starts with `AIza...`)

**Free tier**: 15 requests/minute, 1500 requests/day

### 2. SerpAPI
**Purpose**: Google search results

**How to get**:
1. Visit [SerpAPI](https://serpapi.com/)
2. Sign up for free account
3. Copy API key from dashboard

**Free tier**: 100 searches/month

### 3. Notion API
**Purpose**: Create pages in Notion

**How to get**:
1. Visit [Notion Integrations](https://www.notion.so/my-integrations)
2. Click "New integration"
3. Name it "n8n Research Bot"
4. Copy "Internal Integration Token"
5. **Share your target page** with this integration

**Get Parent Page ID**:
1. Open target Notion page in browser
2. Copy the URL: `https://www.notion.so/workspace/PAGE_ID?...`
3. Extract the 32-character ID (e.g., `abc123def456...`)

---

## 🚀 Installation Steps

### Step 1: Import Workflow to n8n

1. Open n8n (self-hosted or cloud)
2. Click "+" → "Import from File"
3. Select `design-pattern-research-workflow.json`
4. Workflow will appear with 13 nodes

### Step 2: Configure Credentials

#### A. Gemini API Credential

1. Click on any "Gemini" node (e.g., "Gemini Query Optimizer")
2. Click "Credential to connect with"
3. Create new credential:
   - **Type**: HTTP Header Auth
   - **Name**: `Gemini API`
   - **Header Name**: `x-goog-api-key`
   - **Header Value**: `YOUR_GEMINI_API_KEY`

**OR** update the workflow to use a simpler approach:

Replace credential reference with direct key:
```json
"headerParameters": {
  "parameters": [
    {
      "name": "x-goog-api-key",
      "value": "YOUR_GEMINI_API_KEY_HERE"
    }
  ]
}
```

#### B. SerpAPI Credential

1. Click "SerpAPI Search" node
2. Update the `api_key` parameter:
```json
"queryParameters": {
  "parameters": [
    {
      "name": "api_key",
      "value": "YOUR_SERPAPI_KEY_HERE"
    }
  ]
}
```

#### C. Notion API Credential

1. Click "Create Notion Page" node
2. Click "Credential to connect with"
3. Create new credential:
   - **Type**: Notion API
   - **Name**: `Notion API`
   - **API Key**: `YOUR_NOTION_INTEGRATION_TOKEN`
4. Update `pageId` parameter:
```json
"pageId": {
  "__rl": true,
  "mode": "id",
  "value": "YOUR_PARENT_PAGE_ID"
}
```

### Step 3: Install cheerio (for HTML parsing)

The "Parse HTML Content" node uses cheerio library.

**For n8n Cloud**: Already included ✅

**For self-hosted n8n**:
```bash
# Inside n8n Docker container
npm install cheerio

# Or add to package.json in n8n custom modules
```

### Step 4: Test the Workflow

1. Click "Execute Workflow" button
2. When prompted, enter a pattern name:
   - Example: `Redux Toolkit`
   - Or: `React Context API`
   - Or: `Custom Hooks`
3. Watch execution progress (check green checkmarks)
4. Expected duration: ~60-90 seconds
5. Check your Notion page for the new document!

---

## 🎯 Workflow Structure

```
Manual Trigger
  ↓
Set Pattern Input (stores pattern name)
  ↓
Gemini Query Optimizer (generates 3 search queries)
  ↓
Parse Queries (extracts JSON array)
  ↓
SerpAPI Search (loops 3x, gets 5 results each)
  ↓
Filter & Rank Results (prioritizes official docs, picks top 5)
  ↓
Scrape Content (loops 5x, fetches HTML)
  ↓
Parse HTML Content (extracts main text with cheerio)
  ↓
Aggregate Content (merges all scraped content)
  ↓
[PARALLEL EXECUTION]
  ├─ Gemini Content Analyzer (creates structured guide)
  └─ Gemini Code Generator (creates code example)
  ↓
Format for Notion (converts to Notion blocks)
  ↓
Create Notion Page (final output)
```

---

## ⚙️ Customization Options

### Change Search Result Count

In "SerpAPI Search" node:
```json
{
  "name": "num",
  "value": "5"  // Change to 3, 7, or 10
}
```

### Change Content Length

In "Parse HTML Content" node:
```javascript
.substring(0, 15000); // Change to 10000 or 20000
```

### Modify Analysis Format

In "Gemini Content Analyzer" node, update the prompt template to add/remove sections.

### Add Error Handling

Add "On Error" connections to critical nodes:
1. Right-click node → "Add Error Workflow"
2. Connect to a "Send Email" or "Slack" notification node

---

## 🐛 Troubleshooting

### Error: "Failed to extract queries"

**Cause**: Gemini response format changed
**Fix**: Check "Gemini Query Optimizer" output and update regex in "Parse Queries" node

### Error: "cheerio is not defined"

**Cause**: cheerio not installed
**Fix**: Install cheerio (see Step 3 above)

### Error: "403 Forbidden" on scraping

**Cause**: Website blocks automated requests
**Fix**:
- Check "Scrape Content" User-Agent header
- Add delays between requests (Split In Batches node)
- Some sites can't be scraped - the workflow will use snippet instead

### Error: Notion "validation_error"

**Cause**: Invalid block format
**Fix**:
- Check that Parent Page ID is correct
- Ensure integration is shared with the page
- Verify all text fields are strings

### Gemini API "Resource Exhausted"

**Cause**: Rate limit exceeded (15 req/min)
**Fix**:
- Wait 1 minute
- Add "Wait" node (10 seconds) between Gemini calls
- Use lower-frequency tier or paid plan

### SerpAPI "429 Too Many Requests"

**Cause**: Free tier limit (100/month) exceeded
**Fix**:
- Upgrade to paid plan
- Use Google Custom Search API instead
- Cache search results in Google Sheets

---

## 💡 Usage Tips

### Best Patterns to Research

Works best with:
- ✅ React patterns (Redux, Context, Hooks)
- ✅ JavaScript patterns (Observer, Factory, Singleton)
- ✅ Architecture patterns (MVC, MVVM, Clean Architecture)

Less effective with:
- ❌ Very new patterns (< 6 months old, limited docs)
- ❌ Proprietary patterns (company-specific, no public info)
- ❌ Vague terms (use specific names)

### Batch Processing

To research multiple patterns:
1. Replace "Manual Trigger" with "Google Sheets Trigger"
2. Create sheet with pattern names in column A
3. Workflow runs automatically for each row

### Cost Estimation

Per execution (1 pattern):
- Gemini API: 3 requests (free tier)
- SerpAPI: 3 searches ($0.015 on paid tier)
- Notion API: 1 request (free)

**Total**: ~$0.015 per pattern (if using SerpAPI paid tier)

---

## 📊 Output Example

**Input**: "Redux Toolkit"

**Notion Page Created**:
```
Redux Toolkit - Design Pattern
  📋 Overview
  Redux Toolkit is the official, opinionated, batteries-included toolset...

  🔑 Key Concepts
  - Simplified store setup with configureStore()
  - Immer integration for immutable updates
  - Built-in Redux Thunk for async logic
  ...

  ✅ Advantages
  - Reduces boilerplate code by 70%
  - Built-in best practices
  - Excellent TypeScript support

  ⚠️ Disadvantages
  - Learning curve for Redux concepts
  - Overkill for small apps
  ...

  💡 Use Cases
  1. Large-scale apps with complex state
  2. Multiple shared state consumers
  ...

  ⚙️ Setup Guide
  1. npm install @reduxjs/toolkit react-redux
  2. Create store with configureStore()
  ...

  💻 Code Example
  ```typescript
  import { configureStore, createSlice } from '@reduxjs/toolkit';

  // Create a slice
  const counterSlice = createSlice({
    name: 'counter',
    initialState: { value: 0 },
    reducers: {
      increment: (state) => {
        state.value += 1; // Immer handles immutability
      }
    }
  });
  ...
  ```

  🔗 Sources
  • Official Redux Toolkit Docs: https://redux-toolkit.js.org/
  • GitHub Repository: https://github.com/reduxjs/redux-toolkit
  ...

  Generated on: 2025-11-14T12:00:00.000Z
```

---

## 🔄 Next Steps

1. **Test with different patterns**:
   - Redux Toolkit
   - React Context API
   - SWR for data fetching
   - React Query
   - Zustand

2. **Extend the workflow**:
   - Add Slack notification on completion
   - Store results in Airtable for tracking
   - Generate comparison tables for multiple patterns

3. **Optimize performance**:
   - Add caching layer (Redis/Supabase)
   - Implement parallel scraping (Split In Batches)
   - Use webhook trigger for API integration

---

## 📞 Support

**Issues with this workflow?**
- Check n8n execution logs for detailed errors
- Verify all API keys are valid
- Test each node individually (right-click → "Execute Node")

**Common Questions**:
- Q: Can I use OpenAI instead of Gemini?
- A: Yes! Replace Gemini nodes with OpenAI HTTP Request nodes (same prompt structure)

- Q: Does this work for non-React patterns?
- A: Yes! Just update the prompt in "Gemini Content Analyzer" to match your domain

- Q: Can I customize the Notion page format?
- A: Yes! Edit the "Create Notion Page" node blockUi parameter to add/remove sections

---

## 📄 License

This workflow is provided as-is for educational and personal use.

**Attribution**: If you share or modify this workflow, please credit the original design.

---

**Happy Researching! 🚀**
