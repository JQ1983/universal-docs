---
description: Paper component for Universal Dashboard
---

# Paper

**In Material Design, the physical properties of paper are translated to the screen.**

The background of an application resembles the flat, opaque texture of a sheet of paper, and an application’s behavior mimics paper’s ability to be re-sized, shuffled, and bound together in multiple sheets.

## Paper

![](../../../../.gitbook/assets/image%20%2867%29.png)

```text
New-UDPaper -Elevation 0 -Content {} 
New-UDPaper -Elevation 1 -Content {} 
New-UDPaper -Elevation 3 -Content {}
```

## Square Paper

By default, paper will have rounded edges. You can reduce the rounding by using a square paper.

```text
New-UDPaper -Square -Content {}
```

## Colored Paper

The `-Style` parameter can be used to color paper. Any valid CSS can be included in the hashtable for a style.

The following example creates paper with a red background.

```text
New-UDPaper  -Content { } -Style @{ 
     backgroundColor = 'red'
}
```

**New-UDPaper**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Children | ScriptBlock | The content of this paper element. | false |
| Width | String | The width of this paper. | false |
| Height | String | The height of this paper. | false |
| Square | SwitchParameter | Whether this paper is square. | false |
| Style | Hashtable | The CSS style to apply to this paper. | false |
| Elevation | Int32 | The elevation of this paper. | false |

