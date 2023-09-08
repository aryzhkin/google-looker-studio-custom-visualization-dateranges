# Custom Visualization Looker Studio: fixing non-existing `DataRanges`

## Issue
Google's documentation for Looker Studio [says](https://developers.google.com/looker-studio/visualization/library-reference#data) that we can access the `dataRanges` object (which contains the dates selected in the current report to filter the data on that report) via `data.dataRanges`.

But, unfortunately, this is not the case.

This makes it impossible to interact with `dataRanges` when working with native [Comminuty Visualization components](https://developers.google.com/looker-studio/visualization) code.

Below is an example of how to fix this.

## Solution

**Be careful!** After making changes, you will be able to interact with the selected period through `data.customDataRanges` (not `data.dataRanges`).

To fix it, we need to make changes to the `dscc.min.js` (from [this doc](https://developers.google.com/looker-studio/visualization/library)) code.

Just replace the code in this file with [fixed_min.js](https://github.com/aryzhkin/google-looker-studio-custom-visualization-dateranges/blob/48f3cda2b9cb5a2c0a90c6aecc2db66ae187e324/fixed_min.js).

Or you can insert this line yourself from the `fixed_unminified.js` file:
- For `tableTransform`
https://github.com/aryzhkin/google-looker-studio-custom-visualization-dateranges/blob/fab34ac1143672072bb28570ef88f2a8f77ffcb8/fixed_unminified.js#L205-L208
- For `objectTransform`
https://github.com/aryzhkin/google-looker-studio-custom-visualization-dateranges/blob/fab34ac1143672072bb28570ef88f2a8f77ffcb8/fixed_unminified.js#L230-L233

### Simple usage example
```
function drawViz(data) {
  console.log(data.customDataRanges);
}

dscc.subscribeToData(drawViz, { transform: dscc.tableTransform });
```

## References
- https://developers.google.com/looker-studio/visualization/library-reference#data
- https://developers.google.com/looker-studio/visualization/library
- https://stackoverflow.com/questions/76962670/not-receiving-daterange-objects-via-dscc

## About me
I specialize in:
- No-code/low-code tools: like Zapier, make.com & so on
- Google: Sheets, Drive, Gmail, Calendar, Cloud Console, Google Apps Scripts (GAS), Looker Studio (Data Studio)
- Chrome extensions

Feel free to contact with me on the Upwork: [my profile](https://www.upwork.com/fl/~01c9651f77aea190cf).