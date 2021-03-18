---
description: Date Picker component for Universal Dashboard
---

# Date Picker

Date pickers pickers provide a simple way to select a single value from a pre-determined set.

Date pickers can be used in [Forms](form.md) and [Steppers](../navigation/stepper.md).

![](../../../.gitbook/assets/image%20%2873%29.png)

```PowerShell
New-UDDatePicker 
```

## OnChange Event Handler

The OnChange event handler is called when the date changes. You can access the current date by using the `$Body` variable. 

```PowerShell
New-UDDatePicker -OnChange {
    Show-UDToast -Message $body
}
```

## Variant

You can customize how the date picker is show. The default is the `inline` variant that displays the date picker popup inline with the input control. You can also use the `dialog` variant that pops the date picker up in the middle of the screen. Finally, the `static` variant displays the date picker without having to click anything. 

```PowerShell
New-UDDatePicker -Variant static
```

**New-UDDatePicker**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Label | String | The label to show next to the date picker. | false |
| Variant | String | The theme variant to apply to the date picker. | false |
| DisableToolbar | SwitchParameter | Disables the date picker toolbar. | false |
| OnChange | Endpoint | A script block to call with the selected date. The $EventData variable will be the date selected. | false |
| Format | String | The format of the date when it is selected. | false |
| Value | DateTime | The current value of the date picker. | false |

