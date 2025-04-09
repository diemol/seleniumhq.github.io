---
title: Waiting with Expected Conditions
linkTitle: Expected Conditions
weight: 1
description: |
  These are classes used to describe what needs to be waited for.
---

Expected Conditions are used with [Explicit Waits]({{< ref "../waits#explicit-waits" >}}).
Instead of defining the block of code to be executed with a _lambda_, an expected
conditions method can be created to represent common things that get waited on. Some
methods take locators as arguments, others take elements as arguments.

These methods can include conditions such as:

- element exists
- element is stale
- element is visible
- text is visible
- title contains specified value

{{< tabpane text=true >}}
{{< badge-code >}}
{{< tab header="Python" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="CSharp" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}
