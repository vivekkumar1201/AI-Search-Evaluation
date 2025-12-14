# Testing Google Chrome AI Search Mode

This guide explains how to use the evaluation framework to test Google Chrome's AI search mode.

## Setup

### 1. Install Dependencies

```bash
npm install
```

This will install Puppeteer, which is used for browser automation.

### 2. Configuration

The framework is already configured to use Chrome mode by default. You can verify this in `eval/ai-search/config.js`:

```javascript
searchClient: {
  mode: 'chrome', // Use 'chrome' to test Chrome's AI search
  chromeHeadless: true, // Set to false to see the browser
  chromePath: null // Optional: specify Chrome executable path
}
```

### 3. Environment Variables (Optional)

You can also set these via environment variables:

```bash
# Use Chrome mode (default)
export SEARCH_MODE=chrome

# Show browser window (for debugging)
export CHROME_HEADLESS=false

# Specify Chrome path (if Chrome is not in default location)
export CHROME_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
```

## Running the Evaluation

### CLI Mode

```bash
# Run evaluation with Chrome
npm run eval

# Or explicitly set mode
SEARCH_MODE=chrome npm run eval
```

### GUI Mode

```bash
npm start
```

Then open `http://localhost:3000` and run evaluations through the web interface.

## How It Works

1. **Browser Automation**: Uses Puppeteer to launch Chrome
2. **Google Search**: Navigates to Google Search with your query
3. **AI Answer Extraction**: Attempts to extract AI-generated answers from:
   - AI Overview / SGE (Search Generative Experience)
   - Knowledge panels
   - Featured snippets
   - "People also ask" sections
4. **Result Extraction**: Extracts top 10 search results with titles, URLs, and snippets
5. **Evaluation**: Compares results against expected keywords/answers

## Chrome Path Configuration

### macOS
```bash
export CHROME_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
```

### Linux
```bash
export CHROME_PATH="/usr/bin/google-chrome"
# or
export CHROME_PATH="/usr/bin/chromium-browser"
```

### Windows
```bash
export CHROME_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
```

## Troubleshooting

### Chrome Not Found
If Puppeteer can't find Chrome, you can:
1. Install Chrome/Chromium
2. Set `CHROME_PATH` environment variable
3. Or let Puppeteer download Chromium automatically (first run may take time)

### Headless Mode Issues
If you encounter issues, try running with visible browser:
```bash
CHROME_HEADLESS=false npm run eval
```

### Rate Limiting
Google may rate limit if you run too many queries quickly. The evaluator includes delays between queries, but you may need to increase them in `config.js`:

```javascript
evaluation: {
  delay: 500, // Increase delay between queries (ms)
}
```

### AI Features Not Detected
Chrome's AI search features (like AI Overview) may not always be available:
- They depend on your location
- They may require being signed into Google
- Some queries may not trigger AI features

The evaluator will still extract regular search results even if AI answers aren't found.

## Switching Back to API Mode

To use a custom API instead of Chrome:

```bash
export SEARCH_MODE=api
export AI_SEARCH_API_ENDPOINT="http://your-api-endpoint/api/search"
```

Or edit `eval/ai-search/config.js` and set `mode: 'api'`.

