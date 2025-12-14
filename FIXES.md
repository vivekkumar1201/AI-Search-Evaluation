# Fixes Applied

## Dependency Updates

### 1. Multer
- **Before**: `^1.4.5-lts.1` (deprecated, has vulnerabilities)
- **After**: `^2.0.0` (latest, patched)
- **Impact**: No code changes needed - API is compatible

### 2. Puppeteer
- **Before**: `^21.5.0` (deprecated, < 24.15.0 no longer supported)
- **After**: `^24.15.0` (latest supported version)
- **Impact**: Better Chrome automation support

### 3. Node.js Engine Requirement
- **Before**: `>=14.0.0`
- **After**: `>=18.0.0`
- **Reason**: 
  - Fetch API is built-in (used in search-client.js)
  - Puppeteer 24.x requires Node 18+
  - Better performance and security

## Code Improvements

### 1. Lazy Loading Chrome Client
- **Issue**: Chrome client was loaded even when not using Chrome mode
- **Fix**: Changed to lazy-load only when `mode === 'chrome'` and actually needed
- **Benefit**: Faster startup when using API mode, no Puppeteer dependency loaded unnecessarily

### 2. Consistent Default Mode
- Config defaults to `'chrome'` mode
- Search client respects config mode
- Can be overridden via `SEARCH_MODE` environment variable

## Installation

After these fixes, run:

```bash
npm install
```

This will install:
- ✅ Multer 2.x (secure, patched)
- ✅ Puppeteer 24.x (supported version)
- ✅ All other dependencies

## Verification

To verify everything works:

```bash
# Test Chrome mode (default)
npm run eval

# Test API mode
SEARCH_MODE=api npm run eval
```

## Notes

- **Node.js 18+ required**: Make sure you have Node.js 18 or higher
- **First Puppeteer run**: May download Chromium (~170MB) on first use
- **Chrome path**: If Chrome isn't found, Puppeteer will use bundled Chromium

