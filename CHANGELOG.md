# Piwik Platform Changelog

This is a changelog for Piwik platform developers. All changes for our HTTP API's, Plugins, Themes, etc will be listed here.

## Piwik 2.5.0

### Breaking Changes
* The [settings](http://developer.piwik.org/guides/piwik-configuration) API will receive the actual entered value and will no longer convert characters like `&` to `&amp;`. If you still want this behavior - for instance to prevent XSS - you can define a filter by setting the `transform` property like this:
  `$setting->transform = function ($value) { return Common::sanitizeInputValue($value); }`
* Config setting `disable_merged_assets` moved from `Debug` section to `Development`. The updater will automatically change the section for you.
* `API.getRowEvolution` will throw an exception if a report is requested that does not have a dimension, for instance `VisitsSummary.get`. This is a fix as an invalid format was returned before see [#5951](https://github.com/piwik/piwik/issues/5951)

### Deprecations
The following events are considered as deprecated and the new structure should be used in the future. We have not scheduled when those events will be removed but probably in Piwik 3.0 which is not scheduled yet and won't be soon. New features will be added only to the new classes.

* `API.getReportMetadata`, `API.getSegmentDimensionMetadata`, `Goals.getReportsWithGoalMetrics`, `ViewDataTable.configure`, `ViewDataTable.getDefaultType`: use [Report](http://developer.piwik.org/api-reference/Piwik/Plugin/Report) class instead to define new reports. There is an updated guide as well [Part1](http://developer.piwik.org/guides/getting-started-part-1)
* `WidgetsList.addWidgets`: use [Widgets](http://developer.piwik.org/api-reference/Piwik/Plugin/Widgets) class instead to define new widgets
* `Menu.Admin.addItems`, `Menu.Reporting.addItems`, `Menu.Top.addItems`: use [Menu](http://developer.piwik.org/api-reference/Piwik/Plugin/Menu) class instead
* `TaskScheduler.getScheduledTasks`: use [Tasks](http://developer.piwik.org/api-reference/Piwik/Plugin/Tasks) class instead to define new tasks
* `Tracker.recordEcommerceGoal`, `Tracker.recordStandardGoals`, `Tracker.newConversionInformation`: use [Conversion Dimension](http://developer.piwik.org/api-reference/Piwik/Plugin/Dimension/ConversionDimension) class instead
* `Tracker.existingVisitInformation`, `Tracker.newVisitorInformation`, `Tracker.getVisitFieldsToPersist`: use [Visit Dimension](http://developer.piwik.org/api-reference/Piwik/Plugin/Dimension/VisitDimension) class instead
* `ViewDataTable.addViewDataTable`: This event is no longer needed. Visualizations are automatically discovered if they are placed within a `Visualizations` directory inside the plugin.

### New features

#### Translation search
As a plugin developer you might want to reuse existing translation keys. You can now find all available translations and translation keys by opening the page "Settings => Development:Translation search" in your Piwik installation. Read more about [internationalization](http://developer.piwik.org/guides/internationalization) here.

#### Reporting API
* It is now possible to use the `filter_sort_column` parameter when requesting `Live.getLastVisitDetails`. For instance `&filter_sort_column=visitCount`. 

### New APIs
* [Report](http://developer.piwik.org/api-reference/Piwik/Plugin/Report) to add a new report
* [Action Dimension](http://developer.piwik.org/api-reference/Piwik/Plugin/Dimension/ActionDimension) to add a dimension that tracks action related information
* [Visit Dimension](http://developer.piwik.org/api-reference/Piwik/Plugin/Dimension/VisitDimension) to add a dimension that tracks visit related information
* [Conversion Dimension](http://developer.piwik.org/api-reference/Piwik/Plugin/Dimension/ConversionDimension) to add a dimension that tracks conversion related information
* [Dimension](http://developer.piwik.org/api-reference/Piwik/Columns/Dimension) to add a basic non tracking dimension that can be used in `Reports`
* [Widgets](http://developer.piwik.org/api-reference/Piwik/Plugin/Widgets) to add or modfiy widgets
* [Menu](http://developer.piwik.org/api-reference/Piwik/Plugin/Menu) to add or modify menu items
* [Tasks](http://developer.piwik.org/api-reference/Piwik/Plugin/Tasks) to add scheduled tasks

### New commmands
* `generate:theme` Let's you easily generate a new theme and customize colors, see the [Theming guide](http://developer.piwik.org/guides/theming)
* `generate:update` Let's you generate an update file
* `generate:report` Let's you generate a report
* `generate:dimension` Let's you enhance the tracking by adding new dimensions
* `generate:menu` Let's you generate a menu class to add or modify menu items
* `generate:widgets` Let's you generate a widgets class to add or modify widgets
* `generate:tasks` Let's you generate a tasks class to add or modify tasks
* `development:enable` Let's you enable the development mode which will will disable some caching to make code changes directly visible and it will assist developers by performing additional checks to prevent for instance typos. Should not be used in production.
* `development:disable` Let's you disable the development mode 

<!--
## Temlate: Piwik version number

### Breaking Changes
### Deprecations
### New features
### New APIs
### New commmands
### New guides
 -->