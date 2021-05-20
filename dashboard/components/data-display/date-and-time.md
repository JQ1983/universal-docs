---
description: Date and time component for Universal Dashboard.
---

# Date and Time

The `New-UDDateTime` component is used for formatting dates and times within the client's browser. By using the client's browser, you can format the time based on the local time zone and locale settings for the user.

The date and time component uses DayJS. For a full list of custom formatting options, visit the [DayJS documentation](https://day.js.org/docs/en/display/format).

## Basic Formatting

By default, the date and time will be formatted using the `LLL` localized formatting template.

```text
New-UDDateTime -InputObject (Get-Date)
```

Resulting output: August 16, 2018 8:02 PM

## Custom Formatting

You can specify custom formatting strings using the [DayJS formatting template](https://day.js.org/docs/en/display/format).

```text
New-UDDateTime -InputObject (Get-Date) -Format 'DD/MM/YYYY'
```

Resulting output: 25/01/2019

## API

**New-UDDateTime**

| **Name** | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | ID of this component. | False |
| InputObject | string | The date and time to format. | True |
| Format | string | The DayJS format string. | False |
| LocalizedFormat | string | The DayJS localized formatting string. | False |

