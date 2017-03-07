---
title: "Option Views"
excerpt: "Index of option views you can use to allow users to configure your bundle."
---

You can get access to the parameters output by these views on the `config.scene.options` object and use them within your bundle code anywhere you have access to the `config` object (generally within the `create` function of a component or in `bundle.config()`).

## AnnotationTextOptionsView
Displays a textarea accepting a maximum of 280 characters. Returns the contents as `text`.

## AutoRefreshOptionsView
Displays a slider labelled "Refresh URL" which the user can slide between Never (0) and Every 60s. Returns the position as an integer as `refreshRate`.

## AverageLineOptionsView
Displays a checkbox labelled "Show average line" and a text input for "Number of days". If the checkbox is checked, returns the days as an integer as `averageLineDays`.

## BlacklistedWordsView
Displays a control to allow backlisted words to be entered one at a time. Returns the words entered as `blacklistedWords`.

## BundleAuthOptionsView
Displays a list of existing tokens for a specified provider, as well as the option to add a new one. Returns the selected token as `[provider name]`.

## CategoryBreakdownLineTypeOptionsView
Displays a dropdown list of possible chart types: Doughnut, Spline, or Stacked Column. Returns the option selected as `catBreakdownChartType`.

## CategoryOptionsView
Displays a dropdown of the categories associated with the chosen data source. Returns the category or categories selected as `category`.

## CombinedQueryControlsNoCategoryFiltersOptionsView
The same as **CombinedQueryControlsOptionsView**, but without the category filters.

## CombinedQueryControlsNoLocationFiltersOptionsView
The same as **CombinedQueryControlsOptionsView**, but without the location filters.

## CombinedQueryControlsOptionsView
Implements **MinimalControlsOptionsView**, and shows `combinedQueryInputs` and `dateInputs`.

## CompareWithPreviousDaysOptionsView
Displays a field allowing the user to enter a number of days prior to the chosen date range to compare with. Returns the number as `daysPriorToDateRange`.

## CsvFileOptionsView
Displays controls for the upload and selection of a CSV file, returning a JSON specific to this control.

## CustomWordsView
Displays an interface for adding individual custom words. Returns the words entered as `customWords`.

## GenericCustomComponentOptionsView
Displays a custom form input based on supplied config parameters `label`, `inputType`, `paramName`, and `required`. Returns the value entered as `[paramName]`.

## GeocoderOptionsView
Displays controls to enter a location or its coordinates. Returns `geocoderOptions` containing `location` and `coordinates`.

## GlobeScenesControlsOptionsView
Implements **MinimalControlsOptionsView**, and shows only `combinedQueryInputs`.

## GlobeTypeOptionsView
Displays radio buttons allowing the user to choose between a textured or flat globe. Returns their choice as `globeType`.

## GoogleAnalyticsViewIdOptionsView
Displays controls for the user to choose Google Analytics information to use. Returns their selections as `accountId`, `propertyId`, and `viewId`.

## HeaderOptionsView
Displays a checkbox to control the display of the header. Returns a boolean as `showHeader`.

## HideNeutralOptionsView
Displays a checkbox to control whether or not neutral data is shown in sentiment displays. Returns a boolean as `hideNeutral`.

## HighlightSnippetOptionsView
Displays a checkbox to "Highlight search terms". Returns a boolean as `highlightSnippet`.

## ImageBackgroundSizeOptionsView
Displays radio buttons to select the type of image scaling, either "fill tile" or "shrink-to-fit". Returns the selected option as `hasBackGroundSizeContain`.

## ImageUrlOptionsView
Displays a textbox where the user can enter the URL of an image to load in the tile. Returns the path as `imagePath`.

## JsonChartTypeOptionsView
Displays a dropdown where a user can select the style of chart to use: spline, doughnut, or bar chart. Returns the selected option as `jsonChartType`.

## JsonShowLegendOptionsView
Displays a checkbox to indicate whether the chart legend should be shown. Returns a boolean as `jsonShowLegend`.

## JsonUrlOptionsView
Displays a button to Select JSON Feed that brings up a modal when clicked where the user is able to enter the path to their JSON source. Returns the URL as `jsonUrl`.

## MapColouringOptionsView
Displays a dropdown where the user can select whether a map should be colored with sentiment or default colors. Returns the selection as `mapColouring`.

## MapStyleOptionsView
Displays a drpdown to allow the user to choose between dark and light map styles. Returns their selection as `mapStyle`.

## MentionsViewerSortTypeOptionsView
Displays a dropdown of data to sort by with the options "Most Recent Tweets", "Most Recent", "High Influence People", "Most Popular Tweets", and "Most Recent Instagram Posts". Returns the selection as `orderBy`.

## MinimalControlsOptionsView
A unified base control _that cannot be used directly_ that displays the standard Brandwatch data selection form with Data or Groups, Date range, and Filters. Returns those as `queryId` or `queryGroupId`; `startDate`, `endDate`, and `rollingDateRangeValue`; and `filter`, which may contain:
- `showHelp`
- `queryGroups`
- `queries`
- `canEditQueries`
- `canEditGroups`
- `autocompletePosition`
- `metrics`
- `userId`
- `siteGroups`
- `categories`
- `tags`
- `ownerId`
- `authorGroups`
- `locationGroups`
- `professions`
- `interests`
- `showProfessionFilter`
- `showInterestFilter`
- `queryColourOptions`

## NoDateControlsOptionsView
Implements **MinimalControlsOptionsView**, with the date controls removed.

## ProjectSelectionView
Displays a dropdown of the projects available to this user. Returns their selection as `projectId`.

## QueryControlsOptionsView
Implements **MinimalControlsOptionsView**, and shows only `queryInputs`.

## QuerySelectionView
Displays a dropdown allowing the user to select a query associated with the selected project. Returns the selection as `queryId`.

## ReplayAnimationOptionsView
Displays a checkbox to indicate whether an animation should go back to the start after it's run. Returns a boolean as `replayAnimation`.

## SalesforceApiUrlOptionsView
Displays a textbox where the user can enter a URL. Returns the path entered as `salesforceApiUrl`.

## SalesforceCacheTTLInputOptionsView
Inserts a hidden field containing a detault Time to Live. Returns the data as `ttl`.

## SalesforceDepthOptionsView
Displays a dropdown of aggregation depths with the options "Grand Total Only", "First Level", "Second Level", and "Third Level". Returns the selected option as `depth`.

## SalesforceReportFieldNameInputOptionsView
Displays a textbox where the user can enter a Report Field. Returns a string as `fieldName`.

## SalesforceReportIdInputOptionsView
Displays a textbox where the user can enter a Report ID. Returns a string as `reportId`.

## SalesforceXAxisLabelInputOptionsView
Displays a textbox where the user can provide a label for a chart's X-axis. Returns the result as `xAxisTitle`.

## SalesforceYAxisLabelInputOptionsView
Displays a textbox where the user can provide a label for a chart's Y-axis. Returns the result as `yAxisTitle`.

## SentimentChartNameOptionsView
Displays a textbox to enter the subtitle of a sentiment chart within the tile. Returns a string as `name`.

## ShareOfVoiceControlsOptionsView
Implements **MinimalControlsOptionsView**, and shows `combinedQueryInputs` and `dateInputs`.

## ShowNeutralOptionsView
Displays a checkbox to indicate whether to show neutral sentiment data. Returns a boolean as `showNeutral`.

## ShowPercentagesOptionsView
Displays a checkbox to indicate whether data should be shown in percentages rather than totals. Returns a boolean as `showNeutral`.

## TileHeaderOptionsView
Displays a textbox to set the header of the tile, which is populated by default with the type of tile. Returns a string as `name`.

## TopCategoriesCategoryOptionsView
The same as **CategoryOptionsView** but explicitly allows multiple categories to be selected and ony shows parent categories.

## TopTileAnimateOptionsView
Displays a dropdown with options for how a list of top results is displayed: "Bars", "Table", or "Slideshow". Returns the option selected as `topTileAnimationType`.

## TopicColouringOptionsView
Displays a dropdown with options for how topics are colored: "None", "Sentiment", or "Colourful". Returns the selected option as `topicColouring`.

## TopicsTileLayoutOptionsView
Displays a dropdown with options for how topics are displayed: "Cloud", "Bars", or "History". Returns the selected option as `topicsTileLayoutType`.

## UrlOptionsView
Displays a textbox to enter a URL. Returns the path provided as `url`.

## VideoUrlOptionsView
Displays a textbox to enter the URL of a video. Returns the path as `url`.

## WeatherUnitsOptionsView
Displays radio buttons allowing the user to select Celsius or Fahrenheit as temperature display units. Returns the selection as `units`.

## generateCustomComponentOptionsView
An interface to **GenericCustomComponentOptionsView**, adding the ability to use custom component controls.

## /customcomponents
These controls shouldn't be used directly, although they can be used via **generateCustomComponentOptionsView** by giving one of them as the `inputType`.
