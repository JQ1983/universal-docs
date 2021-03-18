---
description: AppBar component for Universal Dashboard
---

# AppBar

**The App Bar displays information and actions relating to the current screen.**

The top App Bar provides content and actions related to the current screen. It's used for branding, screen titles, navigation, and actions.

## AppBar with Custom Drawer

![](../../../.gitbook/assets/image%20%2877%29.png)

```PowerShell
$Drawer = New-UDDrawer -Children {
    New-UDList -Children {
        New-UDListItem -Label "Home"
        New-UDListItem -Label "Getting Started" -Children {
            New-UDListItem -Label "Installation" -OnClick {}
            New-UDListItem -Label "Usage" -OnClick {}
            New-UDListItem -Label "FAQs" -OnClick {}
            New-UDListItem -Label "System Requirements" -OnClick {}
            New-UDListItem -Label "Purchasing" -OnClick {}
        }
    }
}

New-UDAppBar -Position relative -Children { New-UDElement -Tag 'div' -Content { "Title" } } -Drawer $Drawer
```



**New-UDAppBar**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Drawer | Hashtable | A drawer that can be opened from this AppBar. Use New-UDDrawer to create a drawer to pass to this parameter. | false |
| Children | ScriptBlock | Children of this AppBar. The children of an AppBar are commonly text and buttons. | false |
| Position | String | The position of this AppBar. A fixed position will override the default AppBar. | false |

