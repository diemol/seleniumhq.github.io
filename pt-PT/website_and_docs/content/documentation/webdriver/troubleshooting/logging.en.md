---
title: Logging Selenium commands
linkTitle: Logging
weight: 4
description: |
  Getting information about Selenium execution.
---

Turning on logging is a valuable way to get extra information that might help you determine
why you might be having a problem.

## Getting a logger

{{< tabpane text=true >}}

{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L31" >}}

{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L5" >}}

To save logs to a file, you can do this:

```py
log_path = '/path/to/log'
handler = logging.FileHandler(log_path)
logger.addHandler(handler)
```

To display logs in the console, you can do this:

```py
handler = logging.StreamHandler()
logger.addHandler(handler)
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET logger is managed with a static class, so all access to logging is managed simply by referencing `Log` from the `OpenQA.Selenium.Internal.Logging` namespace.
{{% /tab %}}
{{% tab header="Ruby" %}}
If you want to see as much debugging as possible in all the classes,
you can turn on debugging globally in Ruby by setting `$DEBUG = true`.

For more fine-tuned control, Ruby Selenium created its own Logger class to wrap the default `Logger` class.
This implementation provides some interesting additional features.
Obtain the logger directly from the `#logger`class method on the `Selenium::WebDriver` module:

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L11" >}}

```javascript
const logging = require('selenium-webdriver/lib/logging')
logger = logging.getLogger('webdriver')
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

## Logger level

Logger level helps to filter out logs based on their severity.

{{< tabpane text=true >}}

{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L32-L35" >}}

{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L7" >}}

To always output logs with PyTest you need to run with additional arguments.
First, `-s` to prevent PyTest from capturing the console.
Second, `-p no:logging`, which allows you to override the default PyTest logging settings so logs can
be displayed regardless of errors.

So you need to set these flags in your IDE, or run PyTest on command line like:

```bash
pytest -s -p no:logging
```

Finally, since you turned off logging in the arguments above, you now need to add configuration to
turn it back on:

```py
logging.basicConfig(level=logging.WARN)
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET has 6 logger levels: `Error`, `Warn`, `Info`, `Debug`, `Trace` and `None`. The default level is `Info`.

{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Troubleshooting/LoggingTest.cs#L18" >}}

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L13" >}}

To change the level of the logger:

```javascript
logger.setLevel(logging.Level.INFO)
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

### Actionable items

Things are logged as warnings if they are something the user needs to take action on. This is often used
for deprecations. For various reasons, Selenium project does not follow standard Semantic Versioning practices.
Our policy is to mark things as deprecated for 3 releases and then remove them, so deprecations
may be logged as warnings.

{{< tabpane text=true >}}

Example:

```text
May 08, 2023 9:23:38 PM dev.selenium.troubleshooting.LoggingTest logging
WARNING: this is a warning
```

{{% /tab %}}
{{% tab header="Python" %}}
Python logs actionable content at logger level — `WARNING`
Details about deprecations are logged at this level.

Example:

```text
WARNING  selenium:test_logging.py:23 this is a warning
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET logs actionable content at logger level `Warn`.

Example:

```text
11:04:40.986 WARN LoggingTest: this is a warning
```

{{% /tab %}}
{{% tab header="Ruby" %}}
Ruby logs actionable content at logger level — `:warn`.
Details about deprecations are logged at this level.

For example:

```text
2023-05-08 20:53:13 WARN Selenium [:example_id] this is a warning 
```

  {{< tab header="JavaScript" >}}
  {{< alert-content >}}
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

### Useful information

This is the default level where Selenium logs things that users should be aware of but do not need to take actions on.
This might reference a new method or direct users to more information about something

{{< tabpane text=true >}}

Example:

```text
May 08, 2023 9:23:38 PM dev.selenium.troubleshooting.LoggingTest logging
INFO: this is useful information
```

{{% /tab %}}
{{% tab header="Python" %}}
Python logs useful information at logger level — `INFO`

Example:

```text
INFO     selenium:test_logging.py:22 this is useful information
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET logs useful information at logger level `Info`.

Example:

```text
11:04:40.986 INFO LoggingTest: this is useful information
```

{{% /tab %}}
{{% tab header="Ruby" %}}
Ruby logs useful information at logger level — `:info`.

Example:

```text
2023-05-08 20:53:13 INFO Selenium [:example_id] this is useful information 
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

### Debugging Details

The debug log level is used for information that may be needed for diagnosing issues and troubleshooting problems.

{{< tabpane text=true >}}

Example:

```text
May 08, 2023 9:23:38 PM dev.selenium.troubleshooting.LoggingTest logging
FINE: this is detailed debug information
```

{{% /tab %}}
{{% tab header="Python" %}}
Python logs debugging details at logger level — `DEBUG`

Example:

```text
DEBUG    selenium:test_logging.py:24 this is detailed debug information
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET logs most debug content at logger level `Debug`.

Example:

```text
11:04:40.986 DEBUG LoggingTest: this is detailed debug information
```

{{% /tab %}}
{{% tab header="Ruby" %}}
Ruby only provides one level for debugging, so all details are at logger level — `:debug`.

Example:

```text
2023-05-08 20:53:13 DEBUG Selenium [:example_id] this is detailed debug information 
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

## Logger output

Logs can be displayed in the console or stored in a file. Different languages have different defaults.

{{< tabpane text=true >}}

{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L37-L38" >}}
{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L9-L10" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Troubleshooting/LoggingTest.cs#L20" >}}

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L15" >}}

To send logs to console output:

```javascript
logging.installConsoleHandler()
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

## Logger filtering

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L40-L41" >}}
  {{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L12-L13" >}}
  {{< /tab >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Troubleshooting/LoggingTest.cs#L22-L23" >}}

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#17" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L18" >}}
  {{< tab header="JavaScript" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}
