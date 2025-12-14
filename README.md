# AI Search Quality Evaluator

A comprehensive evaluation framework for AI Search quality metrics with a web-based GUI interface. Evaluate your AI Search implementation (including Google Chrome's AI search) with automated testing, detailed metrics, and visual reports.

## Features

- **Quality Metrics**: Evaluate relevance, accuracy, completeness, and performance
- **Test Set Management**: Default test sets + user-uploaded custom test sets (QnA format)
- **Web GUI**: Intuitive browser-based interface with real-time progress tracking
- **CLI Mode**: Command-line interface for CI/CD integration
- **Chrome Browser Automation**: Test Google Chrome's AI search mode using Puppeteer
- **Comprehensive Reports**: JSON and HTML reports with detailed breakdowns
- **Agent Answer Display**: See what the AI agent answered for each query
- **Failed Metric Highlighting**: Visual indicators for metrics that failed thresholds

## Quick Start

### Installation

```bash
npm install
```

### Configuration

**For Chrome AI Search Mode (Default):**
```bash
# Already configured - just run!
npm start
```

**For Custom API:**
```bash
export SEARCH_MODE=api
export AI_SEARCH_API_ENDPOINT="http://your-api-endpoint/api/search"
export AI_SEARCH_API_KEY="your-api-key"
```

Or edit `eval/ai-search/config.js` directly.

**Chrome Mode Options:**
```bash
# Show browser window (for debugging)
export CHROME_HEADLESS=false

# Specify Chrome path (if needed)
export CHROME_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
```

### Running the GUI

```bash
npm start
```

Then open your browser to `http://localhost:3000`

### Running CLI Evaluation

```bash
# Use default test set
npm run eval

# Use all test sets (default + custom)
npm run eval:all

# Use only custom test sets
npm run eval:custom

# Use specific test set
node eval/ai-search/evaluator.js --test-set test-sets/my-set.json
```

## Project Structure

```
.
├── eval/
│   └── ai-search/
│       ├── test-queries.json      # Default test dataset
│       ├── test-sets/              # User-uploaded test sets
│       ├── evaluator.js            # Main evaluation script
│       ├── metrics/                # Metric calculators
│       ├── utils/                  # Utilities
│       └── config.js               # Configuration
├── gui/
│   ├── server.js                   # Express server
│   └── public/                     # Frontend files
├── reports/                         # Generated reports
└── package.json
```

## Test Set Formats

### Default Format

```json
{
  "queries": [
    {
      "id": "q1",
      "query": "What is the capital of France?",
      "expected_keywords": ["Paris", "capital", "France"],
      "expected_answer": "Paris",
      "category": "factual",
      "difficulty": "easy",
      "topic": "geography"
    }
  ]
}
```

### QnA Format (for uploads)

```json
{
  "name": "My Test Set",
  "queries": [
    {
      "question": "What is the capital of France?",
      "answer": "Paris",
      "id": "q1"
    }
  ]
}
```

## Metrics

- **Relevance** (0-1): How well results match query intent
  - Keyword matching, ranking quality, semantic similarity
- **Accuracy** (0-1): Correctness of AI-generated answers
  - Factual correctness, answer quality scoring
- **Completeness** (0-1): Coverage of information in results
  - Result count, topic coverage, information depth
- **Performance** (0-1): Response time and speed
  - Time to first result, total response time

**Mode-Specific Thresholds:**
- **Chrome Mode**: More lenient thresholds (relevance: 0.5, completeness: 0.4, performance: 0.3)
- **API Mode**: Stricter thresholds (all: 0.7)

## Results Display

- **Agent Answers**: See what the AI agent answered for each query
- **Failed Metrics Highlighting**: Visual red highlighting for metrics below thresholds
- **Expandable Details**: Click any row to see full answer and failed metrics
- **Weighted Scoring**: Balanced evaluation considering metric importance

## Testing Chrome AI Search

This framework can evaluate Google Chrome's AI search mode using browser automation. See [CHROME_SETUP.md](CHROME_SETUP.md) for detailed setup instructions.

**Quick Start:**
```bash
# Default mode is Chrome
npm run eval

# Or explicitly
SEARCH_MODE=chrome npm run eval
```

## CI/CD Integration

The project includes a GitHub Actions workflow (`.github/workflows/eval.yml`) that runs evaluations on push/PR.

**Configure secrets:**
- `AI_SEARCH_API_ENDPOINT`: Your API endpoint (if using API mode)
- `AI_SEARCH_API_KEY`: Your API key (if using API mode)
- `SEARCH_MODE`: Set to `chrome` or `api` (default: `chrome`)

## Documentation

- [CHROME_SETUP.md](CHROME_SETUP.md) - Chrome AI search setup guide
- [DISPLAY_UPDATES.md](DISPLAY_UPDATES.md) - Display features documentation
- [FAILURE_ANALYSIS.md](FAILURE_ANALYSIS.md) - Understanding evaluation results

## Requirements

- Node.js 18+ (for fetch API and Puppeteer 24+)
- Chrome/Chromium (for Chrome mode) - Puppeteer will download if not found

## License

MIT

