---
title: Changelog
---

### Develop


### 0.13.25
* [FEATURE] Pass on meta-data from expectation json to validation result json (#2881) (Thanks @sushrut9898)
* [FEATURE] Add sqlalchemy engine support for `column.most_common_value` metric (#3020) (Thanks @shpolina)
* [BUGFIX] Added newline to CLI message for consistent formatting (#3127) (Thanks @ismaildawoodjee)
* [BUGFIX] fix pip install snowflake build error with python 3.9 (#3119) (Thanks @jdimatteo)
* [BUGFIX] Populate (data) asset name in data docs for RuntimeDataConnector (#3105) (Thanks @ceshine)
* [DOCS] Correct path to docs_rtd/changelog.rst (#3120) (Thanks @jdimatteo)
* [DOCS] Fix broken links in "How to write a 'How to Guide'" (#3112)
* [DOCS] Port over "How to add comments to Expectations and display them in DataDocs" from RTD to Docusaurus (#3078)
* [DOCS] Port over "How to create a Batch of data from an in memory Spark or Pandas DF" from RTD to Docusaurus (#3099)
* [DOCS] Update CLI codeblocks in create_your_first_expectations.md (#3106) (Thanks @ories)
* [MAINTENANCE] correct typo in docstring (#3117)
* [MAINTENANCE] DOCS/GDOC-130/Add Changelog (#3121)
* [MAINTENANCE] fix docstring for expectation "expect_multicolumn_sum_to_equal" (previous version was not precise) (#3110)
* [MAINTENANCE] Fix typos in docstrings in map_metric_provider partials (#3111)
* [MAINTENANCE] Make sure that all imports use column_aggregate_metric_provider (not column_aggregate_metric). (#3128)
* [MAINTENANCE] Rename column_aggregate_metric.py into column_aggregate_metric_provider.py for better code readability. (#3123)
* [MAINTENANCE] rename ColumnMetricProvider to ColumnAggregateMetricProvider (with DeprecationWarning) (#3100)
* [MAINTENANCE] rename map_metric.py to map_metric_provider.py (with DeprecationWarning) for a better code readability/interpretability (#3103)
* [MAINTENANCE] rename table_metric.py to table_metric_provider.py with a deprecation notice (#3118)
* [MAINTENANCE] Update CODE_OF_CONDUCT.md (#3066)
* [MAINTENANCE] Upgrade to modern Python syntax (#3068) (Thanks @cclauss)

### 0.13.24
* [FEATURE] Script to automate proper triggering of Docs Azure pipeline (#3003)
* [BUGFIX] Fix an undefined name that could lead to a NameError (#3063) (Thanks @cclauss)
* [BUGFIX] fix incorrect pandas top rows usage (#3091)
* [BUGFIX] Fix parens in Expectation metric validation method that always returned True assertation (#3086) (Thanks @morland96)
* [BUGFIX] Fix run_diagnostics for contrib expectations (#3096)
* [BUGFIX] Fix typos discovered by codespell (#3064) (Thanks cclauss)
* [BUGFIX] Wrap get_view_names in try clause for passing the NotImplemented error (#2976) (Thanks @kj-9)
* [DOCS] Ensuring consistent style of directories, files, and related references in docs (#3053)
* [DOCS] Fix broken link to example DAG (#3061) (Thanks fritz-astronomer)
* [DOCS] GDOC-198 cleanup TOC (#3088)
* [DOCS] Migrating pages under guides/miscellaneous (#3094) (Thanks @spbail)
* [DOCS] Port over “How to configure a new Checkpoint using test_yaml_config” from RTD to Docusaurus
* [DOCS] Port over “How to configure an Expectation store in GCS” from RTD to Docusaurus (#3071)
* [DOCS] Port over “How to create renderers for custom Expectations” from RTD to Docusaurus
* [DOCS] Port over “How to run a Checkpoint in Airflow” from RTD to Docusaurus (#3074)
* [DOCS] Update how-to-create-and-edit-expectations-in-bulk.md (#3073)
* [MAINTENANCE] Adding a comment explaining the IDENTITY metric domain type. (#3057)
* [MAINTENANCE] Change domain key value from “column” to “column_list” in ExecutionEngine implementations (#3059)
* [MAINTENANCE] clean up metric errors (#3085)
* [MAINTENANCE] Correct the typo in the naming of the IDENTIFICATION semantic domain type name. (#3058)
* [MAINTENANCE] disable snowflake tests temporarily (#3093)
* [MAINTENANCE] [DOCS] Port over “How to host and share Data Docs on GCS” from RTD to Docusaurus (#3070)
* [MAINTENANCE] Enable repr for MetricConfiguration to assist with troubleshooting. (#3075)
* [MAINTENANCE] Expand test of a column map metric to underscore functionality. (#3072)
* [MAINTENANCE] Expectation anonymizer supports v3 expectation registry (#3092)
* [MAINTENANCE] Fix -- check for column key existence in accessor_domain_kwargsn for condition map partials. (#3082)
* [MAINTENANCE] Missing import of SparkDFExecutionEngine was added. (#3062)


### Older Changelist
Older changelist can be found at [https://github.com/great-expectations/great_expectations/blob/develop/docs_rtd/changelog.rst](https://github.com/great-expectations/great_expectations/blob/develop/docs_rtd/changelog.rst)
