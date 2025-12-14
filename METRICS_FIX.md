# Metrics Capture Fix

## Issues Found and Fixed

### 1. **Incomplete Summary Calculation**
- **Problem**: GUI server was using a simplified summary that didn't calculate `averageScores` or `overallPassed`
- **Fix**: Now uses the proper `calculateSummary()` function from evaluator.js
- **Result**: Summary now includes all required fields for the frontend

### 2. **Hardcoded Pass Status**
- **Problem**: All queries were marked as `passed: true` regardless of actual metrics
- **Fix**: Now uses `checkQueryPassed()` to properly evaluate metrics against thresholds
- **Result**: Pass/fail status is now accurate

### 3. **Missing Metric Details**
- **Problem**: Results didn't include category, difficulty, and performance details
- **Fix**: Added full result structure matching CLI evaluator
- **Result**: Complete metric information is now captured

## What Was Fixed

### `gui/server.js`
- ✅ Imports `calculateSummary` and `checkQueryPassed` from evaluator
- ✅ Uses proper summary calculation with averageScores
- ✅ Properly checks if queries pass thresholds
- ✅ Includes debugging logs for first query
- ✅ Closes browser after evaluation completes

### `eval/ai-search/evaluator.js`
- ✅ Exports `checkQueryPassed` function for reuse

## Testing the Fix

After restarting the server, you should see:

1. **Proper Metrics**: Average scores should show actual values (not 0.000)
2. **Correct Status**: Overall status should reflect actual pass/fail based on metrics
3. **Chart Data**: The metrics chart should display properly
4. **Accurate Pass Rate**: Should match the actual evaluation results

## Debugging

If metrics are still showing 0.000, check:

1. **Chrome Search Results**: 
   - Are results being extracted? Check server console logs
   - First query will log sample response structure

2. **Google Search Selectors**:
   - Google may have changed their HTML structure
   - Check if `.g`, `.VwiC3b` selectors still work
   - May need to update `chrome-search-client.js` selectors

3. **Rate Limiting**:
   - Google may be blocking automated requests
   - Try running with visible browser: `CHROME_HEADLESS=false npm start`
   - Add delays between queries in config

4. **Network Issues**:
   - Check if Chrome can access Google Search
   - Verify no firewall/proxy blocking

## Next Steps

1. **Restart the server**:
   ```bash
   npm start
   ```

2. **Run a new evaluation** through the GUI

3. **Check server console** for debug logs showing:
   - Sample search response structure
   - Sample calculated metrics

4. **If still showing 0.000**, the issue is likely:
   - Chrome search not returning results (selector issues)
   - Google blocking automated access
   - Network/connectivity problems

## Expected Behavior

After fix, you should see:
- ✅ Average scores with actual values (0.0 to 1.0)
- ✅ Overall status based on actual metrics
- ✅ Chart displaying metric bars
- ✅ Pass rate matching actual results

